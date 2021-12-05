## Instructions Part 3 - Hardware Setup + GUI Extras

1. Bluetooth Support

        $ sudo pacman -S bluez bluez-utils blueman pulseaudio-bluetooth ell
        $ sudo nano /etc/bluetooth/main.conf
- Change: 

        [Policy]
        AutoEnable=true

- Enable Service:

        $ sudo systemctl enable bluetooth.service
        $ sudo systemctl start bluetooth.service
        $ sudo systemctl enable blueman-mechanism
        $ sudo systemctl start blueman-mechanism

2. Wireless Support

        $ sudo pacman -S dkms broadcom-wl-dkms wpa_supplicant

3. Webcam Support


        $ paru -S facetimehd-firmware bcwc-pcie-git
        $ sudo reboot


4. Keyboard light and auto-adjust on ambient light

        $ paru -S kbdlight macbook-lighter

        $ sudo systemctl enable --now macbook-lighter
        $ sudo macbook-lighter-ambient
