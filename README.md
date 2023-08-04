# Configuration for Ubuntu 23.04 Gnome minimal

This guide outlines my personalized configuration for a minimal installation of [Ubuntu 23.04](https://ubuntu.com/) featuring the [Gnome 4](https://www.gnome.org/) desktop environment.
If you're interested in obtaining the official ISO file, you can access it [here](https://ubuntu.com/download/desktop).
Originally, this configuration was tailored for [Manjaro 22.1.3](https://manjaro.org/) with the minimalist [Gnome 4](https://www.gnome.org/) desktop.
However, due to stability concerns, I migrated from Manjaro to Ubuntu on July 30, 2023.
For those curious about the initial setup for Manjaro, you can locate the git tag ([v0.1](https://github.com/le-chartreux/linux-config/tree/v0.1)) associated with the last Manjaro-supporting commit.

This configuration primarily involves executing Shell commands, simplifying the installation and customization processes by eliminating the need for intricate navigation within settings menus.
You can effortlessly employ the commands provided below by copying and pasting them.
It's worth mentioning that while most parts can be handled via these commands, certain aspects might still require adjustments through graphical utilities.

To ensure a seamless setup experience, I recommend commencing with the tools featured in the [Utilities](#utilities) and [Installers](#installers) sections, as these tools might prove indispensable for other facets of the configuration process.

## Table of contents

<!-- TOC -->

- [Configuration for Ubuntu 23.04 Gnome minimal](#configuration-for-ubuntu-2304-gnome-minimal)
  - [Table of contents](#table-of-contents)
  - [Global](#global)
    - [Installers](#installers)
      - [apt](#apt)
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
    - [Vanilla desktop](#vanilla-desktop)
    - [Button layout](#button-layout)
    - [Extensions](#extensions)
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
    - [Keybindings](#keybindings)
  - [Dev](#dev)
    - [Git](#git)
    - [GitHub](#github)
    - [Applications](#applications)
      - [Visual Studio Code](#visual-studio-code)
      - [Pycharm pro](#pycharm-pro)
    - [Zsh](#zsh)
      - [Oh My Zsh](#oh-my-zsh)
  - [Misc applications](#misc-applications)
    - [Social](#social)
      - [Discord](#discord)
    - [Graphisme](#graphisme)
      - [Gimp](#gimp)
    - [Utilities](#utilities)

<!-- /TOC -->

## Global

### Installers

#### [apt](https://wiki.debian.org/Apt)

A package manager utilized in [Debian](https://www.debian.org/) and its derivatives, including Ubuntu.

```sh
# Update the system
sudo apt update && sudo apt upgrade && sudo apt autoremove
```

#### [snap](https://ubuntu.com/core/services/guide/snaps-intro)

An official application store provided by [Canonical](https://canonical.com/), enabling developers to distribute their applications.

```sh
# Update snap packages
sudo snap refresh
```

#### [Flatpak](https://flathub.org/)

A comprehensive app repository, useful to obtain applications not found in [apt](https://wiki.debian.org/Apt) or [snap](https://ubuntu.com/core/services/guide/snaps-intro).

```sh
# Install Flatpak
sudo apt install flatpak
# Integrate Flatpak with Gnome Software
sudo apt install gnome-software-plugin-flatpak
# Add Flathub repository for applications
sudo flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
# Restart your computer after making these changes
```

#### [Gnome Software](https://apps.gnome.org/app/org.gnome.Software/)

The official Gnome installer, offering an aesthetic alternative to the [Canonical's snap store](https://ubuntu.com/core/docs/store-overview) while featuring the same applications.

```sh
# Install Gnome Software
sudo apt install gnome-software
```

#### [pip](https://pypi.org/project/pip/)

A package installer essential for [Python](https://www.python.org/) applications. Many applications depend on it; installing it is crucial for their usage.

```sh
# Install pip for Python
sudo apt install python3-pip
```

#### [pipx](https://pypa.github.io/pipx/)

The recommended approach for installing [Python](https://www.python.org/) applications from [pip](#pip). This method ensures each application resides within an isolated virtual environment, preventing conflicts with the system's [Python](https://www.python.org/) environment.

```sh
# Install pipx for managing Python applications
sudo apt install pipx
```

### System

```sh
# enabling TRIM (for better SSD performances)
sudo systemctl enable fstrim.timer
sudo systemctl start fstrim.timer
```

### Text

#### Spellcheckers

```sh
# english
sudo apt install aspell-en
sudo apt install libmythes-1.2-0
sudo apt install mythes-en-us 
sudo snap install languagetool
# french
sudo apt install aspell-fr mythes-fr
```

#### Fonts

```sh
# glacial indifference (a cool font)
wget https://www.fontsquirrel.com/fonts/download/glacial-indifference --output-document=glacial-indifference.zip
unzip glacial-indifference.zip -d glacial-indifference
font-manager --install glacial-indifference/*.otf
rm -r glacial-indifference.zip glacial-indifference
```

## [Gnome 4](https://www.gnome.org/)

### Vanilla desktop

To get the vanilla Gnome 4 desktop (without the Ubuntu-look) on top of which the riced desktop will be build, execute the following commands:

```sh
sudo apt install gnome-session
sudo apt install gnome-software
# then reboot your computer and select 'Gnome' as a desktop at the logging page instead of 'Ubuntu'
```

### Button layout

Get the minimize and maximize buttons on the windows.

```sh
gsettings set org.gnome.desktop.wm.preferences button-layout "'appmenu:minimize,maximize,close'"
```

### Extensions

```sh
# tool to manage extensions
flatpak run com.mattjakeman.ExtensionManager
# tool to install from cli
pipx install gnome-extensions-cli --system-site-packages 
```

#### [User Themes](https://extensions.gnome.org/extension/19/user-themes/)

Allow to use shell themes.

```sh
gext install user-theme@gnome-shell-extensions.gcampax.github.com
```

#### [Blur my Shell](https://github.com/aunetx/blur-my-shell)

Add a blur effect.

```sh
gext install blur-my-shell@aunetx
dconf write /org/gnome/shell/extensions/blur-my-shell/panel/blur false
dconf write /org/gnome/shell/extensions/blur-my-shell/overview/style-components 3
```

#### [Caffeine](https://github.com/eonpatapon/gnome-shell-extension-caffeine)

Pause screen saving.

```sh
gext install caffeine@patapon.info
```

#### [Dash to Dock](https://micheleg.github.io/dash-to-dock/)

Change the dock to a nicer one.

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

Patch glitches on fullscreen (e.g. with the dock not hiding).

```sh
gext install unredirect@vaina.lt
```

#### [Freon](https://github.com/UshakovVasilii/gnome-shell-extension-freon)

Display system temperatures (CPU, disk, video card), voltage and fan RPM.
I use it to display the maximum temperature of the CPUs.

```sh
# freon relies on lm-sensors
sudo apt install lm-sensors
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

Improve the overview, mainly bigger workspaces thumbnails and search box hidden when unused.

```sh
gext install gnome-ui-tune@itstime.tech
```

#### [Just Perfection](https://gitlab.gnome.org/jrahmatzadeh/just-perfection)

Hide some UI elements, change the behavior and customize the desktop.

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

Add round corners to the screen.

```sh
gext install panel-corners@aunetx
dconf write /org/gnome/shell/extensions/panel-corners/screen-corners true
dconf write /org/gnome/shell/extensions/panel-corners/panel-corners true
```

#### [Resource Monitor](https://github.com/0ry0n/Resource_Monitor/)

Show some useful information about the system (RAM & swap usage here).

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

Add rounded corners to apps.

```sh
gext install rounded-window-corners@yilozt
dconf write /org/gnome/shell/extensions/rounded-window-corners/global-rounded-corner-settings "{'padding': <{'left': <uint32 1>, 'right': <uint32 1>, 'top': <uint32 1>, 'bottom': <uint32 1>}>, 'keep_rounded_corners': <{'maximized': <false>, 'fullscreen': <false>}>, 'border_radius': <uint32 6>, 'smoothing': <uint32 1>, 'enabled': <true>}"
```

#### [RunCat](https://github.com/win0err/gnome-runcat)

Indicator of CPU usage with a cat whose running speed depends on CPU load.

```sh
gext install runcat@kolesnikov.se
dconf write /org/gnome/shell/extensions/runcat/idle-threshold 15
```

#### [Transparent Window Moving](https://github.com/Noobsai/transparent-window-moving)

Makes the window semi-transparent when moving or resizing.

```sh
gext install transparent-window-moving@noobsai.github.com
```

### Theme

```sh
# tool to manage themes
sudo apt install gnome-tweaks
# tool to download gnome themes
pipx install gnomelooks
# Sweet-Dark-v40
gnomelooks get https://www.gnome-look.org/p/1253385/
gsettings set org.gnome.desktop.interface gtk-theme Sweet-Dark-v40
gsettings set org.gnome.desktop.wm.preferences theme Sweet-Dark-v40
dconf write /org/gnome/shell/extensions/user-theme/name "'Sweet-Dark-v40'"
# Sweet-cursors
gnomelooks get https://www.gnome-look.org/p/1393084/
gsettings set org.gnome.desktop.interface cursor-theme Sweet-cursors
```

### Keybindings

```sh
gsettings set org.gnome.desktop.wm.keybindings close "['<Shift><Super>q']"
gsettings set org.gnome.desktop.wm.keybindings begin-move "['<Super>m']"
gsettings set org.gnome.desktop.wm.keybindings maximize "['<Super>Up']"
gsettings set org.gnome.settings-daemon.plugins.media-keys terminal "['<Super>Return']"
gsettings set org.gnome.settings-daemon.plugins.media-keys help "[]"
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-1 "['<Super>F1']"
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-2 "['<Super>F2']"
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-3 "['<Super>F3']"
dconf write /org/gnome/desktop/wm/keybindings/move-to-workspace-4 "['<Super>F4']"
dconf write /org/gnome/shell/keybindings/switch-to-application-1 '@as []'
dconf write /org/gnome/shell/keybindings/switch-to-application-2 '@as []'
dconf write /org/gnome/shell/keybindings/switch-to-application-3 '@as []'
dconf write /org/gnome/shell/keybindings/switch-to-application-4 '@as []'
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-1 "['<Super>1']"
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-2 "['<Super>2']"
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-3 "['<Super>3']"
dconf write /org/gnome/desktop/wm/keybindings/switch-to-workspace-4 "['<Super>4']"
# manually add in settings/keyboard/custom shortcuts/ the following:
# - name: 'open monitor'
# - command: 'gnome-system-monitor'
# - shortcut: Ctrl + Shift + Escape  
```

## Dev

### [Git](https://git-scm.com/)

```sh
git config --global user.name "XXX"
git config --global user.email "XXX@XXX"
git config --global core.editor nano
```

### [GitHub](https://github.com/)

```sh
ssh-keygen -t ed25519 -C "your-gh-email@something"
wl-copy < ~/.ssh/id_*.pub
```

Then add it [here](https://github.com/settings/ssh/new).

### Applications

#### [Visual Studio Code](https://code.visualstudio.com/)

Best text editor in my opinion: nice looking, easy and tons of plugins.

```sh
sudo snap install code --classic
```

#### [Pycharm pro](https://www.jetbrains.com/pycharm/)

Best Python IDE in my opinion.

```sh
sudo snap install pycharm-professional --classic
```

### [Zsh](https://wiki.archlinux.org/title/Zsh)

Shell with a lot of cool features and customization.

#### [Oh My Zsh](https://ohmyz.sh/)

Framework to manage [Zsh](https://wiki.archlinux.org/title/Zsh) configuration.

TODO

## Misc applications

### Social

#### [Discord](https://discord.com/)

```sh
sudo snap install discord
# betterdiscord
sudo add-apt-repository ppa:chronobserver/betterdiscordctl
sudo apt update
sudo apt install betterdiscordctl
betterdiscordctl -i snap install
```

### Graphisme

#### [Gimp](https://www.gimp.org/)

```sh
sudo apt install gimp
```

### Utilities

```sh
# allows to get content from the web
# maybe you will need to downgrade libcurl before: sudo apt install libcurl4=7.88.1-8ubuntu2
sudo apt install curl
# allows to copy texts and images to clipboard in command line
sudo apt install wl-clipboard
# allows to manage fonts
sudo apt install font-manager
```
