[Previous Page](/README.md) - [Next Page](/Install-p2.md)

<h1 align="center"> Part I - Base Install (No Dual-Boot using btrfs and snapshots)</h1>

 1. Download the [Arch Linux installer ISO](https://www.archlinux.org/download/).
 2. Create a [bootable installer](https://wiki.archlinux.org/title/USB_flash_installation_medium).
      - [Use DD](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_basic_command_line_utilities) if you are using any linux OS.
      - For Windows I'd use [Rufus](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_Rufus), also opting for DD during the process.
      - If using macOS, also [use DD](https://wiki.archlinux.org/title/USB_flash_installation_medium#Using_macOS_dd) or [Etcher](https://etcher.balena.io).

 3. Boot into installer

    Hold the *alt* key at system boot and pick `efi` usb drive, the yellow icon.
 4. From this point, you can either ssh into the laptop and continue the installation remotely or skip this step and continue.

    Update root password for ssh

    ```shell
    $ passwd 
    ```

    Check ip and ssh in from remote device

    ```shell
    $ ip -c a
    ```

    From client

    ```shell
    $ ssh root@'remote-ip-address'
    ```
 5. Set timedate true

    ```shell
    $ timedatectl set-ntp true
    ```
 6. Disk partitioning

    ```shell
    $ shred -v -n1 /dev/sda
    
    $ gdisk /dev/sda
    
      o 'for new GPT'
      n for new partition +512M  ef00
      n for rest of the drive
      w to save and exit
    ```
 7. Encryption and file system creation

    ```shell
     $ modprobe dm-crypt
     $ cryptsetup benchmark
     $ cryptsetup -c aes-xts-plain -y -s 512 luksFormat /dev/sda2
     $ cryptsetup luksOpen /dev/sda2 lukscrypt
     
     $ mkfs.vfat -F32 -n EFI /dev/sda1
     $ mkfs.btrfs -L ROOT -f -n 32k /dev/mapper/lukscrypt
    
     $ mount /dev/mapper/lukscrypt /mnt
     $ btrfs sub create /mnt/@
     $ btrfs sub create /mnt/@home
     $ btrfs sub create /mnt/@pkg
     $ btrfs sub create /mnt/@snapshots
     $ umount /mnt
    
     $ mount -o noatime,nodiratime,compress=zstd,space_cache=v2,ssd,subvol=@ /dev/mapper/lukscrypt /mnt
    
     $ mkdir -p /mnt/{boot,home,var/cache/pacman/pkg,.snapshots}
    
     $ mount -o noatime,nodiratime,compress=zstd,space_cache=v2,ssd,subvol=@home /dev/mapper/lukscrypt /mnt/home
    
     $ mount -o noatime,nodiratime,compress=zstd,space_cache=v2,ssd,subvol=@pkg /dev/mapper/lukscrypt /mnt/var/cache/pacman/pkg
    
     $ mount -o noatime,nodiratime,compress=zstd,space_cache=v2,ssd,subvol=@snapshots /dev/mapper/lukscrypt /mnt/.snapshots
    
    
     $ mount /dev/sda1 /mnt/boot
    ```
 8. Base Install

    ```shell
    $ pacstrap /mnt base base-devel nano linux-zen linux-zen-headers linux-firmware intel-ucode git btrfs-progs openssh networkmanager
    
    $ genfstab -U -p /mnt >> /mnt/etc/fstab
    $ cat /mnt/etc/fstab
    
    ```
 9. chroot into base install and fine-tune system setup

    ```shell
    $ arch-chroot /mnt
    
     $ nano /etc/mkinitcpio.conf

         add btrfs i915 to MODULES
         change HOOKS line to this=
         HOOKS=(base keyboard udev consolefont autodetect modconf kms keymap encrypt block btrfs filesystems resume fsck)
    
     $ mkinitcpio -P
    
     
     $ echo LANG=en_GB.UTF-8 > /etc/locale.conf
     $ nano /etc/locale.gen <------ unmark your lang, should match locale.conf
     $ locale-gen
     $ echo KEYMAP=us > /etc/vconsole.conf
     $ ln -sf /usr/share/zoneinfo/Africa/Cairo /etc/localtime <---- Change to your timezone
     $ hwclock --systohc
     $ nano /etc/pacman.conf
         uncomment: 
         Color
         VerbosePkgLists
         ParallelDownloads = 5 
         [multilib]
         Include = /etc/pacman.d/mirrorlist
    
     $ echo mba > /etc/hostname
     
    
     $ nano /etc/hosts
         127.0.0.1 localhost
         ::1 localhost
         127.0.1.1 mba.localdomain mba
    
    $ pacman -S efibootmgr network-manager-applet dialog acpi acpi_call acpid wpa_supplicant mtools dosfstools avahi xdg-user-dirs xdg-utils gvfs gvfs-smb nfs-utils inetutils dnsutils bluez bluez-utils alsa-utils pipewire pipewire-alsa pipewire-pulse pipewire-jack pavucontrol bash-completion rsync tlp firewalld nss-mdns ntfs-3g terminus-font mesa vulkan-intel lib32-mesa xf86-video-intel tmux
    
     $ bootctl --path=/boot install
     
     $ nano /boot/loader/loader.conf
         add
         default  arch-zen.conf

     $ blkid -s UUID -o value /dev/sda2
     $ blkid | grep sda2 | cut -d'"' -f 2 > /boot/loader/entries/arch-zen.conf
     $ blkid /dev/mapper/lukscrypt >> /boot/loader/entries/arch-zen.conf
     $ nano /boot/loader/entries/arch-zen.conf
    
         title Arch Linux-Zen
         linux /vmlinuz-linux-zen
         initrd /intel-ucode.img
         initrd /initramfs-linux-zen.img
         options cryptdevice=UUID=*****:root:allow-discards root=UUID=ROOTUUID rootflags=subvol=@ rd.lukscrypt.options=discard rw
     
     $ systemctl enable NetworkManager
     $ systemctl enable sshd.service
     $ systemctl enable fstrim.timer
     $ systemctl enable bluetooth
     $ systemctl enable avahi-daemon
     $ systemctl enable tlp
     $ systemctl enable firewalld
     $ systemctl enable acpid
    
     $ useradd -mG wheel USER
     $ passwd USER
     $ echo "USER ALL=(ALL) ALL" >> /etc/sudoers.d/USER
     
     $ exit
     $ umount -a
     $ reboot
    
    ```
- Remove USB and let your new OS boot, if it doesn't boot, recheck the steps and make sure you wrote or copied all the commands correctly.
- Once booted, you can log in with the credentials you created earlier, and continue to [part II](/Install-p2.md) of this guide.
