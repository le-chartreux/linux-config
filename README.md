# Configuration for Ubuntu 23.04 Gnome minimal

This guide outlines my personalized configuration for a minimal installation of [Ubuntu 23.04](https://ubuntu.com/) with the [Gnome 4](https://www.gnome.org/) desktop environment.
If you're looking for the official ISO file, you can find it [here](https://ubuntu.com/download/desktop).

Initially, this configuration was tailored for [Manjaro 22.1.3](https://manjaro.org/) using the minimalist [Gnome 4](https://www.gnome.org/) desktop.
However, due to stability concerns, I migrated to Ubuntu on July 30, 2023.
If you're interested in the initial Manjaro setup, you can check out the associated git tag ([v0.1](https://github.com/le-chartreux/linux-config/tree/v0.1)) that corresponds to the last Manjaro-supporting commit.

This configuration primarily involves executing Shell commands.
By using these commands, you can simplify the installation and customization processes without needing to navigate intricate settings menus.
ust copy and paste the commands provided below.
Keep in mind that while most tasks can be handled through these commands, certain adjustments may still require graphical utilities.

For a seamless setup experience, I recommend starting with the tools mentioned in the [Utilities](#utilities) and [Installers](#installers) sections.
These tools might be essential for other parts of the configuration process.

## Table of contents

<!-- TOC -->

- [Configuration for Ubuntu 23.04 Gnome minimal](#configuration-for-ubuntu-2304-gnome-minimal)
  - [Table of contents](#table-of-contents)
  - [Global](#global)
    - [Installers](#installers)
      - [apt](#apt)
      - [Nala](#nala)
      - [snap](#snap)
      - [Flatpak](#flatpak)
      - [Gnome Software](#gnome-software)
      - [pip](#pip)
      - [pipx](#pipx)
    - [System](#system)
    - [Text](#text)
      - [Spellcheckers](#spellcheckers)
      - [Fonts](#fonts)
  - [Gnome 4](#gnome-4)
    - [Vanilla Desktop](#vanilla-desktop)
    - [Button Layout](#button-layout)
    - [Tap to click](#tap-to-click)
    - [Workspaces](#workspaces)
    - [Extensions](#extensions)
      - [Managers](#managers)
      - [User Themes](#user-themes)
      - [Blur my Shell](#blur-my-shell)
      - [Caffeine](#caffeine)
      - [Dash to Dock](#dash-to-dock)
      - [Disable unredirect fullscreen windows](#disable-unredirect-fullscreen-windows)
      - [Freon](#freon)
      - [Gnome 4x UI Improvements](#gnome-4x-ui-improvements)
      - [Just Perfection](#just-perfection)
      - [Panel corners](#panel-corners)
      - [Resource Monitor](#resource-monitor)
      - [Rounded Window Corners](#rounded-window-corners)
      - [RunCat](#runcat)
      - [Transparent Window Moving](#transparent-window-moving)
    - [Theme](#theme)
      - [Utils](#utils)
      - [Shell](#shell)
      - [Cursors](#cursors)
      - [Libadwaita](#libadwaita)
      - [Icons](#icons)
      - [Grub](#grub)
    - [Keybindings](#keybindings)
    - [Disable PageUp and PageDown](#disable-pageup-and-pagedown)
  - [Dev](#dev)
    - [Git](#git)
    - [GitHub](#github)
    - [Applications](#applications)
      - [Visual Studio Code](#visual-studio-code)
      - [PyCharm Professional](#pycharm-professional)
    - [Python](#python)
      - [bpython](#bpython) 
  - [CLI](#cli)
    - [Gnome terminal](#gnome-terminal)
    - [Zsh](#zsh)
      - [Oh My Zsh](#oh-my-zsh)
      - [zsh autosuggestions](#zsh-autosuggestions)
      - [zsh syntax highlighting](#zsh-syntax-highlighting)
      - [Spaceship Prompt](#spaceship-prompt)
    - [exa](#exa)
    - [bat](#bat)
  - [Miscellaneous Applications](#miscellaneous-applications)
    - [Social](#social)
      - [Discord](#discord)
    - [Graphics](#graphics)
      - [Gimp](#gimp)
    - [Utilities](#utilities)

<!-- /TOC -->

## Global

### Installers

#### [apt](https://wiki.debian.org/Apt)

A package manager used in [Debian](https://www.debian.org/) and its derivatives, including Ubuntu.

```sh
# Update the system
sudo apt update && sudo apt upgrade && sudo apt autoremove
```

#### [Nala](https://github.com/volitank/nala)

A user-friendly front-end for [apt](https://wiki.debian.org/Apt), offering an improved interface and features like parallel downloads, history and undo.

```sh
sudo apt install nala
# Get the fastest mirror
sudo nala fetch
```

#### [snap](https://ubuntu.com/core/services/guide/snaps-intro)

An official application store by [Canonical](https://canonical.com/), allowing developers to distribute their applications.

```sh
# Update snap packages
sudo snap refresh
```

#### [Flatpak](https://flathub.org/)

A comprehensive app repository, useful to obtain applications not found in [apt](https://wiki.debian.org/Apt) or [snap](https://ubuntu.com/core/services/guide/snaps-intro).

```sh
# Install Flatpak
sudo nala install flatpak
# Integrate Flatpak with Gnome Software
sudo nala install gnome-software-plugin-flatpak
# Add Flathub repository for applications
sudo flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
# Restart your computer after making these changes
```

#### [Gnome Software](https://apps.gnome.org/app/org.gnome.Software/)

The official Gnome installer, offering an aesthetic alternative to the [Canonical's snap store](https://ubuntu.com/core/docs/store-overview) while featuring the same applications.

```sh
# Install Gnome Software
sudo nala install gnome-software
```

#### [pip](https://pypi.org/project/pip/)

A package manager for [Python](https://www.python.org/) applications. Many applications rely on it, making its installation vital.

```sh
# Install pip for Python
sudo nala install python3-pip
```

#### [pipx](https://pypa.github.io/pipx/)

The recommended approach for installing [Python](https://www.python.org/) applications via [pip](#pip).
This method ensures that each application resides within an isolated virtual environment, preventing conflicts with the system's [Python](https://www.python.org/) environment.

```sh
# Install pipx for managing Python applications
sudo nala install pipx
```

### System

Enabling TRIM enhance SSD performance.

```sh
sudo systemctl enable fstrim.timer
sudo systemctl start fstrim.timer
```

### Text

#### Spellcheckers

```sh
# For English
sudo nala install aspell-en
sudo nala install libmythes-1.2-0
sudo nala install mythes-en-us 
sudo snap install languagetool
# For French
sudo nala install aspell-fr mythes-fr
```

#### Fonts

```sh
# Font management tool
sudo nala install font-manager

# Glacial indifference (a cool font)
wget https://www.fontsquirrel.com/fonts/download/glacial-indifference --output-document=glacial-indifference.zip
unzip glacial-indifference.zip -d glacial-indifference
font-manager --install glacial-indifference/*.otf
rm -r glacial-indifference.zip glacial-indifference

# CascadiaCode Nerd
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/CascadiaCode.zip
unzip CascadiaCode.zip -d CascadiaCode
font-manager --install CascadiaCode/*.ttf
rm -r CascadiaCode*

# JetBrainsMono Nerd
wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.0.2/JetBrainsMono.zip
unzip JetBrainsMono.zip -d JetBrainsMono
font-manager --install JetBrainsMono/*.ttf
rm -r JetBrainsMono*
```

## [Gnome 4](https://www.gnome.org/)

### Vanilla Desktop

Acquire the unaltered Gnome 4 desktop (without the Ubuntu appearance) as the foundation for the customized desktop setup.

```sh
sudo nala install gnome-session
sudo nala install gnome-software
# Following this, restart your computer and opt for 'Gnome' as the desktop environment on the login screen, as opposed to 'Ubuntu'
```

### Button Layout

Add minimize and maximize buttons to windows.

```sh
dconf write /org/gnome/desktop/wm/preferences/button-layout "'appmenu:minimize,maximize,close'"
```

### Tap to click

Enable the tap-to-click functionality on your touchpad, making tapping the touchpad equivalent to clicking.

```sh
gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true
```

### Workspaces

Use 4 workspaces by default.

```sh
dconf write /org/gnome/desktop/wm/preferences/num-workspaces 4
dconf write /org/gnome/mutter/dynamic-workspaces false
```

### Extensions

#### Managers

```sh
# Tool to manage extensions
flatpak run com.mattjakeman.ExtensionManager
# Tool to install from cli
pipx install gnome-extensions-cli --system-site-packages 
```

#### [User Themes](https://extensions.gnome.org/extension/19/user-themes/)

Enable the use of custom shell themes.

```sh
gext install user-theme@gnome-shell-extensions.gcampax.github.com
```

#### [Blur my Shell](https://github.com/aunetx/blur-my-shell)

Add an elegant blur effect.

```sh
gext install blur-my-shell@aunetx
dconf write /org/gnome/shell/extensions/blur-my-shell/panel/blur false
dconf write /org/gnome/shell/extensions/blur-my-shell/overview/style-components 3
```

#### [Caffeine](https://github.com/eonpatapon/gnome-shell-extension-caffeine)

Prevent screen saving during activities.

```sh
gext install caffeine@patapon.info
```

#### [Dash to Dock](https://micheleg.github.io/dash-to-dock/)

Enhance the dock's appearance and behavior.

```sh
gext install dash-to-dock@micxgx.gmail.com
dconf write /org/gnome/shell/extensions/dash-to-dock/multi-monitor true
dconf write /org/gnome/shell/extensions/dash-to-dock/intellihide-mode "'ALL_WINDOWS'"
dconf write /org/gnome/shell/extensions/dash-to-dock/animation-time 0.1
dconf write /org/gnome/shell/extensions/dash-to-dock/hide-delay 0.1
dconf write /org/gnome/shell/extensions/dash-to-dock/show-apps-at-top true
dconf write /org/gnome/shell/extensions/dash-to-dock/show-trash false
dconf write /org/gnome/shell/extensions/dash-to-dock/hot-keys false
dconf write /org/gnome/shell/extensions/dash-to-dock/middle-click-action "'launch'"
dconf write /org/gnome/shell/extensions/dash-to-dock/shift-middle-click-action "'quit'"
dconf write /org/gnome/shell/extensions/dash-to-dock/custom-theme-shrink true
dconf write /org/gnome/shell/extensions/dash-to-dock/disable-overview-on-startup true
dconf write /org/gnome/shell/extensions/dash-to-dock/apply-custom-theme false
dconf write /org/gnome/shell/extensions/dash-to-dock/custom-background-color true
dconf write /org/gnome/shell/extensions/dash-to-dock/background-color "'rgb(14,13,31)'"
dconf write /org/gnome/shell/extensions/dash-to-dock/transparency-mode "'DYNAMIC'"
dconf write /org/gnome/shell/extensions/dash-to-dock/customize-alphas true
dconf write /org/gnome/shell/extensions/dash-to-dock/min-alpha 0
dconf write /org/gnome/shell/extensions/dash-to-dock/max-alpha 1
```

#### [Disable unredirect fullscreen windows](https://github.com/kazysmaster/gnome-shell-extension-disable-unredirect)

Prevent glitches during fullscreen operations, such as avoiding the dock from remaining visible.

```sh
gext install unredirect@vaina.lt
```

#### [Freon](https://github.com/UshakovVasilii/gnome-shell-extension-freon)

Monitor system temperatures, voltage, and fan RPMs, particularly beneficial for tracking CPU temperatures.

```sh
# freon relies on lm-sensors
sudo nala install lm-sensors
sudo sensors-detect  # hit enter and type 'yes' at the end to save to /etc/modules
sudo /etc/init.d/kmod start
# restart your computer
gext install freon@UshakovVasilii_Github.yahoo.com 
dconf write /org/gnome/shell/extensions/freon/hot-sensors "['__max__']"
dconf write /org/gnome/shell/extensions/freon/show-rotationrate false
dconf write /org/gnome/shell/extensions/freon/show-voltage false
dconf write /org/gnome/shell/extensions/freon/show-power false
dconf write /org/gnome/shell/extensions/freon/group-rotationrate false
dconf write /org/gnome/shell/extensions/freon/group-voltage false
```

#### [Gnome 4x UI Improvements](https://github.com/axxapy/gnome-ui-tune)

Enhance the overview with larger workspace thumbnails and a hidden search box.

```sh
gext install gnome-ui-tune@itstime.tech
```

#### [Just Perfection](https://gitlab.gnome.org/jrahmatzadeh/just-perfection)

Customize the desktop by hiding UI elements and altering behavior.

```sh
gext install just-perfection-desktop@just-perfection
dconf write /org/gnome/shell/extensions/just-perfection/theme true
dconf write /org/gnome/shell/extensions/just-perfection/activities-button false
dconf write /org/gnome/shell/extensions/just-perfection/app-menu-label false
dconf write /org/gnome/shell/extensions/just-perfection/world-clock false
dconf write /org/gnome/shell/extensions/just-perfection/weather false
dconf write /org/gnome/shell/extensions/just-perfection/events-button false
dconf write /org/gnome/shell/extensions/just-perfection/startup-status 0
dconf write /org/gnome/shell/extensions/just-perfection/animation 4
dconf write /org/gnome/shell/extensions/just-perfection/notification-banner-position 2
```

#### [Panel corners](https://github.com/aunetx/panel-corners)

Introduce rounded corners to the screen edges.

```sh
gext install panel-corners@aunetx
dconf write /org/gnome/shell/extensions/panel-corners/screen-corners true
dconf write /org/gnome/shell/extensions/panel-corners/panel-corners true
```

#### [Resource Monitor](https://github.com/0ry0n/Resource_Monitor/)

Display valuable system information, such as RAM and swap usage.

```sh
gext install Resource_Monitor@Ory0n
dconf write /com/github/Ory0n/Resource_Monitor/cpustatus false
dconf write /com/github/Ory0n/Resource_Monitor/decimalsstatus true
dconf write /com/github/Ory0n/Resource_Monitor/iconsposition "'left'"
dconf write /com/github/Ory0n/Resource_Monitor/diskspacestatus false
dconf write /com/github/Ory0n/Resource_Monitor/diskstatsstatus false
dconf write /com/github/Ory0n/Resource_Monitor/gpustatus false
dconf write /com/github/Ory0n/Resource_Monitor/netethstatus false
dconf write /com/github/Ory0n/Resource_Monitor/netwlanstatus false
dconf write /com/github/Ory0n/Resource_Monitor/ramunit "'perc'"
dconf write /com/github/Ory0n/Resource_Monitor/swapstatus true
dconf write /com/github/Ory0n/Resource_Monitor/swapunit "'perc'"
dconf write /com/github/Ory0n/Resource_Monitor/thermalcputemperaturestatus false
dconf write /com/github/Ory0n/Resource_Monitor/thermalgputemperaturestatus false
```

#### [Rounded Window Corners](https://github.com/yilozt/rounded-window-corners)

Implement rounded corners for application windows.

```sh
gext install rounded-window-corners@yilozt
dconf write /org/gnome/shell/extensions/rounded-window-corners/global-rounded-corner-settings "{'padding': <{'left': <uint32 1>, 'right': <uint32 1>, 'top': <uint32 1>, 'bottom': <uint32 1>}>, 'keep_rounded_corners': <{'maximized': <false>, 'fullscreen': <false>}>, 'border_radius': <uint32 6>, 'smoothing': <uint32 1>, 'enabled': <true>}"
```

#### [RunCat](https://github.com/win0err/gnome-runcat)

Display CPU usage using a running cat whose speed corresponds to CPU load.

```sh
gext install runcat@kolesnikov.se
dconf write /org/gnome/shell/extensions/runcat/idle-threshold 15
```

#### [Transparent Window Moving](https://github.com/Noobsai/transparent-window-moving)

Enable window transparency during movement or resizing.

```sh
gext install transparent-window-moving@noobsai.github.com
```

### Theme

#### Utils

```sh
# Install Gnome Tweaks for theme management
sudo nala install gnome-tweaks
# Install gnomelooks for downloading Gnome themes
pipx install gnomelooks
```

#### Shell

Install the Sweet-Dark-v40 GTK theme.

```sh
gnomelooks get https://www.gnome-look.org/p/1253385/
dconf write /org/gnome/desktop/interface/gtk-theme "'Sweet-Dark-v40'"
dconf write /org/gnome/desktop/wm/preferences/theme "'Sweet-Dark-v40'"
```

#### Cursors

Install the Sweet-cursors theme.

```sh
gnomelooks get https://www.gnome-look.org/p/1393084/
# need to move it else the cursor theme will not apply everywhere 
mv ~/.local/share/icons/Sweet-cursors ~/.icons/
dconf write /org/gnome/desktop/interface/cursor-theme "'Sweet-cursors'"
```

#### Libadwaita

To theme Libadwaita applications, we need to use [Gradiance](https://flathub.org/apps/com.github.GradienceTeam.Gradience).

```sh
sudo flatpak install flathub com.github.GradienceTeam.Gradience
flatpak run com.github.GradienceTeam.Gradience
flatpak run --command=gradience-cli com.github.GradienceTeam.Gradience download --preset-name "Pretty Purple"
flatpak run --command=gradience-cli com.github.GradienceTeam.Gradience apply -n "Pretty Purple"
# then logout 
```

#### Icons

Install the ePapirus-Dark icon theme (purple folders).

```sh
gnomelooks get https://www.gnome-look.org/p/1166289
dconf write /org/gnome/desktop/interface/icon-theme "'ePapirus-Dark'"
```

#### Grub

Install Vimix theme with colors.
See [the github page](https://github.com/vinceliuice/grub2-themes) for futher information about the configuration (e.g. screen resolution).

```sh
git clone https://github.com/vinceliuice/grub2-themes.git
cd grub2-themes/
sudo ./install.sh --theme vimix --icon color --screen 1080p
cd ..
rm -rf grub2-themes
```

### Keybindings

```sh
# Close window with Shift + Super + q
dconf write /org/gnome/desktop/wm/keybindings/close "['<Shift><Super>q']"
# Initiate window move with Super + m
dconf write /org/gnome/desktop/wm/keybindings/begin-move "['<Super>m']"
# Maximize window with Super + Up
dconf write /org/gnome/desktop/wm/keybindings/maximize "['<Super>Up']"
# Launch terminal with Super + Return
dconf write /org/gnome/settings-daemon/plugins/media-keys/terminal "['<Super>Return']"
# Disable Help keybinding
dconf write /org/gnome/settings-daemon/plugins/media-keys/help "'[]'"

# Assign workspace switch shortcuts
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-1 "['<Super>F1']"
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-2 "['<Super>F2']"
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-3 "['<Super>F3']"
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-4 "['<Super>F4']"

# Clear application switch shortcuts
dconf write /org/gnome/shell/keybindings/switch-to-application-1 '@as []'
dconf write /org/gnome/shell/keybindings/switch-to-application-2 '@as []'
dconf write /org/gnome/shell/keybindings/switch-to-application-3 '@as []'
dconf write /org/gnome/shell/keybindings/switch-to-application-4 '@as []'

# Assign workspace switch shortcuts
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-1 "['<Super>1']"
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-2 "['<Super>2']"
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-3 "['<Super>3']"
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-4 "['<Super>4']"
```

For a custom shortcut that opens the system monitor, to mimic Windows 10 behavior, follow these steps in *Settings > Keyboard > Custom Shortcuts*:

- Name: 'Open Monitor'
- Command: 'gnome-system-monitor'
- Shortcut: Ctrl + Shift + Escape

### Disable PageUp and PageDown

I rarely find myself using the PageUp and PageDown keys, and I frequently press them unintentionally.
Therefore, I find it more convenient to disable them.
However, it's worth noting that this approach might not be effective in certain applications like VSCode.
To check which keycode is linked to PageUp and PageDown, use the `xev` command.

```sh
xmodmap -e 'keycode 112 = '
xmodmap -e 'keycode 117 = '
```

## Dev

### [Git](https://git-scm.com/)

Configure your global Git settings.

```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global core.editor nano
```

### [GitHub](https://github.com/)

Generate an SSH key and add it to your GitHub account by pasting the copied key [here](https://github.com/settings/ssh/new).

```sh
ssh-keygen -t ed25519 -C "your-gh-email@something"
wl-copy < ~/.ssh/id_*.pub
```

### Applications

#### [Visual Studio Code](https://code.visualstudio.com/)

My preferred text editor: visually appealing, user-friendly, and enriched with numerous plugins.

```sh
sudo snap install code --classic
```

#### [PyCharm Professional](https://www.jetbrains.com/pycharm/)

My preferred Python IDE.

```sh
sudo snap install pycharm-professional --classic
```

### Python

#### [bpython](https://bpython-interpreter.org/)

An interactive Python shell with many modern features (e.g. autocomplete, colors, nice tabulations).

```sh
pipx install bpython
```

## CLI

### Gnome terminal

In the `Text` configuration, set the font to `CaskaydiaCove Nerd Font Mono` and the initial terminal size to 90 columns.
In the `Colors` configuration, select `Show bold text in bright colors` to increase visibility.

### [Zsh](https://wiki.archlinux.org/title/Zsh)

Shell with a lot of cool features and customization.

```sh
sudo nala install zsh
# do your configuration
zsh
# set zsh as the default shell
chsh -s /bin/zsh `whoami`
# logout
```

#### [Oh My Zsh](https://ohmyz.sh/)

Framework to manage [Zsh](https://wiki.archlinux.org/title/Zsh) configuration.

```sh
# install
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# in .zshrc, replace the 'plugin' line by this one
plugins=(colored-man-pages cp)
```

#### [zsh autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/)

Fish-like autosuggestions for zsh.

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# add zsh-autosuggestions to your plugin list in .zshrc
```

#### [zsh syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting/)

Fish shell like syntax highlighting for Zsh.

```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
# add zsh-syntax-highlighting at the end of your plugin list in .zshrc
```

#### [Spaceship Prompt](https://github.com/spaceship-prompt/spaceship-prompt)

Minimalistic, powerful and extremely customizable Zsh prompt.

```sh
git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
# Set ZSH_THEME="spaceship" in your .zshrc.
```

### [exa](https://the.exa.website/)

Remplacement for `ls`, way more fancy.

```sh
sudo nala install exa
```

### [bat](https://github.com/sharkdp/bat)

Remplacement for `cat`, with syntax hightlighting.

```sh
sudo nala install bat
```

## Miscellaneous Applications

### Social

#### [Discord](https://discord.com/)

```sh
sudo snap install discord
# Install BetterDiscord
sudo add-apt-repository ppa:chronobserver/betterdiscordctl
sudo nala update
sudo nala install betterdiscordctl
betterdiscordctl -i snap install
```

### Graphics

#### [Gimp](https://www.gimp.org/)

GIMP is ugly and hard to learn, but it's a powerful graphics editing software.

```sh
sudo nala install gimp
```

### Utilities

```sh
# Install curl to fetch content from the web
# If needed, you may have to downgrade libcurl before: sudo nala install libcurl4=7.88.1-8ubuntu2
sudo nala install curl

# Install wl-clipboard to copy text and images to clipboard from the command line
sudo nala install wl-clipboard
```
