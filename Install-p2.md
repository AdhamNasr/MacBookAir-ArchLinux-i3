[Previous Page](/Install-p1.md) - [Next Page](/Install-p3.md)
<h1 align="center"> Part II - Post Base System Install - GUI Setup</h1>

1. Install Xorg, i3, & a few extas

    ```Shell
    $ sudo pacman -Syu xorg-xinit xorg-server xorg-xbacklight tilda cpio i3-gaps firefox picom nitrogen lxappearance dolphin rofi obs-studio vlc htop neofetch conky conky-manager zsh zsh-completions zsh-autosuggestions zsh-syntax-highlighting code polkit-kde-agent kdeconnect dunst playerctl dmidecode arc-gtk-theme arc-solid-gtk-theme arc-icon-theme pacman-contrib gnome-keyring polybar
    $ sudo nano /etc/X11/xinit/xinitrc
    ```
    comment out last four and add
    
    ```
    exec i3
    eval $(gnome-keyring-daemon --start)
    export SSH_AUTH_SOCK
    ```
    ```shell
    $ startx
    ```

    - Accept config wizard and press command+shift+e to exit back to the terminal

2.  Console customization

    ```shell
    $ chsh -s /bin/zsh
    
    $ curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh
    
    $ mkdir Git
    $ cd Git
    $ git clone https://github.com/powerline/fonts powerline-fonts
    
    $ cd powerline-fonts
    $ sudo cp -r Terminus/PSF/*.psf.gz /usr/share/kbd/consolefonts
    
    $ sudo nano /etc/vconsole.conf
    ```
    - copy and paste the following to the end of the document
    ```SHELL
    FONT=ter-powerline-v16b
    ```
3.  WM & system customization

    ```
    $ cd Git
    
    $ git clone https://aur.archlinux.org/paru.git
    
    $ cd paru 
    
    $ makepkg -si PKGBUILD 
    
    $ paru -S noto-fonts ttf-material-icons-git termsyn-powerline-font-git ttf-font-awesome timeshift timeshift-autosnap
     
    ```

[Previous Page](/Install-p1.md) - [Next Page](/Install-p3.md)
