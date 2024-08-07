https://askubuntu.com/questions/1513445/how-to-install-latest-version-of-thunderbird-as-a-traditional-deb-package-withou
https://www.debugpoint.com/remove-snap-ubuntu/


# Ubuntu Setup
My personal adjustments for Ubuntu/Linux
- [Add trash icon to Desktop](#trash-icon)
- [Brave Error on APT Repository](#brave-error)
- [Change cursors theme](#change-cursors)
- [Change default emoji shortcut](#default-emoji)
- [Change GRUB background color](#change-grub)
- [Delay on volume change fix](#delay-volume)
- [Disable shutdown confirmation](#shutdown-confirmation)
- [Dual boot Windows-Ubuntu time fix](#time-fix)
- [Enable touch-to-click on login screen](#enable-touch)
- [Font Manager](#font-manager)
- [GRUB Customizer](#grub-customizer)
- [Flameshot for screenshots](#flameshot)
- [Papirus Icon Theme](#papirus-icon)
- [Precise scroll on firefox](#firefox-scroll)
- [Remove Ubuntu PRO Advert](#ubuntu-pro)
- [Slow network](#slow-network)
- [SSH config file example](#ssh-config)
- [Storage manager `ncdu`](#ncdu)
- [Virtual Box Driver Error](#virtual-box)
- [ZSH and Oh My Zsh for terminal](#zsh)

#
### Add trash icon to Desktop<a name="trash-icon"></a>
```
gsettings set org.gnome.shell.extensions.ding show-trash true
```

### Brave Error on APT Repository<a name="brave-error"></a>
https://community.brave.com/t/solved-linux-deb-install-gives-error-when-you-apt-update-a-repository/464626
> N: Skipping acquire of configured file 'main/binary-i386/Packages' as repository 'https://brave-browser-apt-release.s3.brave.com stable InRelease' doesn't support architecture 'i386'
In: `/etc/apt/sources.list.d/brave-browser-release.list`

Add: `arch=amd64` as in:  
```
deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main
```

### Change cursors theme<a name="change-cursors"></a>

Cursors theme: [https://www.gnome-look.org/p/1148692](https://www.gnome-look.org/p/1148692)
Place them unzipped on:

- **User**: /home/user/.icons
- **Root**: /usr/share/icons

It'll be available on distro settings

### Change default emoji shortcut<a name="default-emoji"></a>

On terminal:

```
ibus-setup
```

Remove the default shortcut

### Change GRUB background color<a name="change-grub"></a>

https://askubuntu.com/questions/47488/how-to-change-the-purple-background-color-in-grub  
In `/usr/share/plymouth/themes/default.grub`  
Change `if background_color 20,20,20 ; then`  
To `if background_color 0,0,0 ; then`

### Delay on volume change fix<a name="delay-volume"></a>

https://askubuntu.com/questions/1376719/obnoxious-delay-on-hold-volume-up-down

> open `/etc/pulse/daemon.conf`  
> uncomment and set `enable-deferred-volume=no`  
> on terminal: `pulseaudio -k && pulseaudio --start`

### Disable shutdown confirmation<a name="shutdown-confirmation"></a>
```
gsettings set org.gnome.SessionManager logout-prompt false
```

### Dual boot Windows-Ubuntu time fix<a name="time-fix"></a>

https://mashtips.com/fix-linux-windows-dual-boot-clock-different-time/  
`timedatectl set-local-rtc 1 --adjust-system-clock`

### Font Manager
```
sudo add-apt-repository ppa:font-manager/staging
sudo apt-get update
sudo apt-get install font-manager
```

### Enable touch-to-click on login screen<a name="enable-touch"></a>

Edit

```
/usr/share/X11/xorg.conf.d/40-libinput.conf
```

```
Section "InputClass"
    Identifier "libinput touchpad catchall" # In this scetion/identifier
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
    Driver "libinput"
    Option "Tapping" "on" # Add this
EndSection
```

### Flameshot for screenshots<a name="flameshot"></a>

https://flameshot.org/

### GRUB Customizer<a name="grub-customizer"></a>

```
sudo add-apt-repository ppa:danielrichter2007/grub-customizer
```

```
sudo apt-get update
```

```
sudo apt-get install grub-customizer
```

### Papirus Icon Theme<a name="papirus-icon"></a>

https://github.com/PapirusDevelopmentTeam/papirus-icon-theme

### Slow network
Edit
```
/etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
```   
Change the value from `3` to `2`

### Precise scroll on firefox<a name="firefox-scroll"></a>
https://askubuntu.com/questions/1148934/precise-scrolling-in-firefox

In:
```
/etc/environment
```
Add:
```
MOZ_USE_XINPUT2=1
```
Reboot.

### Remove Ubuntu PRO Advert<a name="ubuntu-pro"></a>
https://askubuntu.com/questions/1434512/how-to-get-rid-of-ubuntu-pro-advertisement-when-updating-apt

```
sudo mv /etc/apt/apt.conf.d/20apt-esm-hook.conf /etc/apt/apt.conf.d/20apt-esm-hook.conf.bak
sudo touch /etc/apt/apt.conf.d/20apt-esm-hook.conf
```
### SSH config file example<a name="ssh-config"></a>
```
/home/user/.ssh/config
```
```
Host hostname
        HostName 192.168.0.1
        User username
        Port 2222
        IdentityFile /path/to/identity/file
```
```
chmod 400 /path/to/identity/file  
```
Then `ssh hostname` to connect

### Storage manager `ncdu`<a name="ncdu"></a>
```
sudo apt install ncdu
```

### Virtual Box Driver Error<a name="virtual-box"></a>
https://forums.virtualbox.org/viewtopic.php?t=110128 

> The VirtualBox Linux kernel driver is either not loaded or not set up correctly. Please try setting it up again by executing '/sbin/vboxconfig'

Install:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/ppa -y
```

```
sudo apt update
```

```
sudo apt install g++-12 gcc-12
```

Run: 
```
sudo /sbin/vboxconfig
```
And continue the setup.

Reboot the PC > At blue screen > Enroll MOK > Yes > Input your password > Reboot

### ZSH and Oh My Zsh for terminal<a name="zsh"></a>

#### Install ZSH

https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH

#### Install Oh My Zsh

https://github.com/ohmyzsh/ohmyzsh

#### Hack font

https://github.com/source-foundry/Hack/releases

#### Dracula Theme

https://draculatheme.com/

#### Zinit

Install:

```
bash -c "$(curl --fail --show-error --silent --location https://raw.githubusercontent.com/zdharma-continuum/zinit/HEAD/scripts/install.sh)"
```

Add basic plugins:

```
zinit light zdharma/fast-syntax-highlighting
zinit light zsh-users/zsh-autosuggestions
zinit light zsh-users/zsh-completions
```

#### Spaceship

```
git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
```

```
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
```

Change `~/.zshrc`

```
ZSH_THEME="spaceship"
```

Create the config file at `/home/user/.spaceshiprc.zsh`, with content:

```
SPACESHIP_PROMPT_ORDER=(
  user          # Username section
  dir           # Current directory section
  host          # Hostname section
  git           # Git section (git_branch + git_status)
  hg            # Mercurial section (hg_branch  + hg_status)
  exec_time     # Execution time
  line_sep      # Line break
  jobs          # Background jobs indicator
  exit_code     # Exit code section
  char          # Prompt character
)
SPACESHIP_USER_SHOW=always
SPACESHIP_PROMPT_ADD_NEWLINE=false
SPACESHIP_CHAR_SYMBOL="❯"
SPACESHIP_CHAR_SUFFIX=" "
```

#### Command not found suggestions
```
sudo apt install command-not-found
```
```
echo "source /etc/zsh_command_not_found" >> ~/.zshrc
```
