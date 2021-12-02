## Instructions Part 2 - Post Base System Install

1. Create user

        # useradd -m user
        # passwd user
        # gpasswd -a user wheel
        # nano /etc/sudoers

- from here I try to keep track of everything happening to the OS so I use [etckeeper][etc] for /etc, and a [bare repo][bare] for ~/home to track changes, other than that it would be overkill, but doable... (follow the links for updated instructions, or skip this step)

[etc]: https://wiki.archlinux.org/title/Etckeeper
[bare]: https://dev.to/bowmanjd/store-home-directory-config-files-dotfiles-in-git-using-bash-zsh-or-powershell-the-bare-repo-approach-35l3 


2. Install Xorg & i3 + extras

        $ sudo pacman -Syu xorg-xinit xorg-server terminator tilda mesa git lib32-mesa xf86-video-intel vulkan-intel cpio i3-gaps reflector

        $ sudo reflector -c Germany -c France -c Italy -a 20 --sort rate --protocol https --save /etc/pacman.d/mirrorlist --verbose
        
        $ sudo nano /etc/X11/xinit/xinitrc

    comment out last four and add `exec i3`

        $ startx

3. Install hardware drivers + extras

        $ sudo pacman -S tmux firefox picom nitrogen lxappearance nautilus rofi simplescreenrecorder pulseaudio-alsa pavucontrol obs-studio vlc htop neofetch nextcloud-client conky conky-manager

4. Console customization

        $ sudo pacman -S zsh zsh-completions zsh-autosuggestions zsh-syntax-highlighting

        $ sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

        $ mkdir Git
        $ cd Git
        $ git clone https://github.com/powerline/fonts powerline-fonts

        $ cd powerline-fonts
        $ sudo cp -r Terminus/PSF/*.psf.gz /usr/share/kbd/consolefonts

        $ sudo nano /etc/vconsole.conf
        FONT=ter-powerline-v16b

        $ git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1

        $ ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"

5. WM customization

        $ cd Git

        $ git clone https://aur.archlinux.org/paru.git 

        $ cd paru 

        $ makepkg -si PKGBUILD 

        $ paru -S polybar noto-fonts ttf-material-icons-git termsyn-powerline-font-git ttf-font-awesome zscroll

        $ sudo pacman -Syu code polkit polkit-kde-agent kdeconnect dunst playerctl dmidecode arc-gtk-theme arc-solid-gtk-theme arc-icon-theme pacman-contrib gnome-keyring


- Clone basic WM customization

        $ scp -r anasr@10.0.0.40:~/.config/i3 ~/.config/
        $ scp -r anasr@10.0.0.40:~/.config/picom ~/.config/
        $ scp -r anasr@10.0.0.40:~/.config/polybar ~/.config/
        $ scp -r anasr@10.0.0.40:~/.config/rofi ~/.config/
        $ scp -r anasr@10.0.0.40:~/.config/tilda ~/.config/

        $ cd ~/.config/polybar

        $ sudo chmod +x launch.sh
        $ cd scripts

        $ sudo chmod +x get_spotify_status.sh
        $ sudo chmod +x network-traffic.sh  
        $ sudo chmod +x scroll_spotify_status.sh

- add to 

        $ sudo nano /etc/X11/xinit/xinitrc

        eval $(gnome-keyring-daemon --start)
        export SSH_AUTH_SOCK

7. And Finally...

        $ sudo reboot