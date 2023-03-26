## Instructions Part 1 - Base Install

[iso]: https://www.archlinux.org/download/
[installer]: https://wiki.archlinux.org/title/USB_flash_installation_medium


 1. Download the [Arch Linux installer ISO][iso].

 2. Create a [bootable installer][installer].

 3. Boot into installer

      Hold the alt key at system boot and pick `efi`
    
 4. Make sure SSD is partitioned from macOS correctly

      Always dual-boot incase of firmware updates from apple
 
 5. From this point you can ssh into the laptop and continue the installation remotely.

      Update root password for ssh

        # passwd
        
      Check ip and ssh in

        # ip -c a
         
 6. Set timedate true

        # timedatectl set-ntp true

 7. Disk partitioning (you should have three partitions on sda if you've done things correctly in macOS)

          # lsblk -fs

          NAME  FSTYPE   FSVER            LABEL       FSAVAIL FSUSE% MOUNTPOINTS
          loop0 squashfs 4.0                                0   100% /run/archiso/airootfs
          sda1  vfat     FAT32            EFI                  
          └─sda                                                      
          sda2  apfs                                                 
          └─sda                                                      
          sda3  vfat     FAT32            ARCHLINUX                  
          └─sda                                                      
          sdb1  iso9660  Joliet Extension ARCH_202111                
          └─sdb iso9660  Joliet Extension ARCH_202111                
          sdb2  vfat     FAT16            ARCHISO_EFI                
          └─sdb iso9660  Joliet Extension ARCH_202111                
          sdc

          # gdisk /dev/sda

          `delete third partition`

          d > 3

          `create new linux partition`
          n > press enter till it's done (4 times)

          w to save and exit

 8. Encryption and filesystem creation

        # modprobe dm-crypt
        # cryptsetup benchmark
        # cryptsetup -c aes-xts-plain -y -s 256 luksFormat /dev/sda3
        # cryptsetup luksOpen /dev/sda3 lvm
        # pvcreate /dev/mapper/lvm
        # vgcreate main /dev/mapper/lvm
        # lvcreate -L 8GB -n swap main
        # lvcreate -l 100%FREE -n root main
        8GB   swap
        52GB  root

        # mkfs.ext4 -L root /dev/mapper/main-root
        # mkswap -L swap /dev/mapper/main-swap
        # mount /dev/mapper/main-root /mnt
        # mkdir /mnt/boot
        # mount /dev/sda1 /mnt/boot

 9. Base Install

        # pacstrap /mnt base base-devel syslinux nano linux-zen linux-zen-headers linux-firmware mkinitcpio lvm2 networkmanager network-manager-applet dialog acpi acpi_call acpid intel-ucode openssh os-prober

        # syslinux-install_update -i -a -m -c /mnt

        # nano /mnt/boot/syslinux/syslinux.cfg
        Change APPEND 
        cryptdevice=/dev/sda3:main root=/dev/mapper/main-root rw lang=en locale=en_GB.UTF-    

        # swapon -L swap
        # genfstab -U -p /mnt >> /mnt/etc/fstab
        # nano /mnt/etc/fstab
        add noatime & discard for root

 10. chroot into base install and fine-tune system setup

          # arch-chroot /mnt
          # echo LANG=en_GB.UTF-8 > /etc/locale.conf
          # nano /etc/locale.gen
          # locale-gen
          # ln -sf /usr/share/zoneinfo/Africa/Cairo /etc/localtime
          # nano /etc/pacman.conf
          uncomment: 
          Color
          VerbosePkgLists
          ParallelDownloads = 3 
          [multilib]
          Include = /etc/pacman.d/mirrorlist

          # pacman -Sy
          # nano /etc/mkinitcpio.conf
          add ext4 to MODULES
          change HOOKS line to this=
          HOOKS=(base udev autodetect keyboard keymap modconf block lvm2 encrypt filesystems fsck)

          # mkinitcpio -P

          # nano /etc/hostname
          mba

          # nano /etc/hosts
          127.0.0.1 localhost
          ::1 localhost
          127.0.1.1 mba.localdomain mba
          
          # systemctl enable NetworkManager
          # systemctl enable sshd.service
          # systemctl enable reflector.timer
          # systemctl enable fstrim.timer
          # systemctl enable acpid
          # bootctl --path=/boot install
          # nano /boot/loader/loader.conf
          replace code with arch-*
          
          # blkid |grep sda3 |cut -d'"' -f 2
          # blkid |grep sda3 |cut -d'"' -f 2 > /boot/loader/entries/arch.conf
          # nano /boot/loader/entries/arch.conf
          title Arch Linux
          linux /vmlinuz-linux-zen
          initrd /intel-ucode.img
          initrd /initramfs-linux-zen.img
          options cryptdevice=UUID=****:lvm root=/dev/mapper/main-root quiet rw

          # passwd
          
          # exit
          # umount /mnt/{boot,}
          # reboot
