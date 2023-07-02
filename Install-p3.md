[Previous Page](//Install-p2.md)
<h1 align="center"> Part III - Hardware Setup + GUI Extras</h1>

1. Bluetooth Support

   ```shell
    $ sudo pacman -S blueman ell
   ```

- Enable Service:

  ```shell
    $ sudo systemctl enable --now blueman-mechanism
  ```

2. Wireless Support

   ```shell
    $ sudo pacman -S dkms broadcom-wl-dkms
   
    $ sudo reboot
   ```
3. Webcam Support

   ```shell
    $ paru -S facetimehd-firmware bcwc-pcie-git
    $ sudo reboot
   ```
4. Keyboard light

   ```shell
    $ paru -S kbdlight macbook-lighter
   
    $ sudo systemctl enable --now macbook-lighter
   ```
5. Polybar, rofi, and GUI customization
   ```shell
    $ paru -S pywal-git ttf-icomoon-feather siji-ng ttf-weather-icons bat noto-fonts-emoji

    $ sudo pacman -S ttf-iosevka-nerd ttf-fantasque-sans-mono ttf-droid ttf-ionicons redshift archlinux-wallpaper calc breeze-icons i3lock libva-intel-driver earlyoom systembus-notify intel-media-sdk libnotify hunspell-en_GB xorg-xwininfo poppler-data libappimage gst-plugins-good gst-libav ffmpegthumbs kdegraphics-thumbnailers kio-admin v4l2loopback-dkms catimg ghostscript libheif x11-ssh-askpass sshfs python-nautilus qt5-tools libnotify vim 
   
    $ cd Git
    $ git clone --depth=1 https://github.com/adi1090x/polybar-themes.git
   
    $ cd polybar-themes
    $ chmod +x setup.sh
    $ ./setup.sh
    $ bash \~/.config/polybar/launch.sh --forest

    $ cd ..
    $ git clone --depth=1 https://github.com/adi1090x/rofi.git
    $ cd rofi
    $ chmod +x setup.sh
    $ ./setup.sh
   ```
6. plymouth

   ```shell
    $ paru -S plymouth
    $ nano /etc/mkinitcpio.conf
    add HOOKS=(...>udev plymouth
    $ sudo nano /boot/loader/entries/arch-zen.conf  
    add quiet splash vt.global_cursor_default=0
    $ sudo mkinitcpio -P
    $ reboot
   ```