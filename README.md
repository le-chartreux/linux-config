# Configuration for Manjaro 22.1.3 Gnome minimal

My personal configuration for [Manjaro](https://manjaro.org/) 22.1.3 minimal with [Gnome 4](https://www.gnome.org/) desktop. You can download the official ISO [here](https://download.manjaro.org/gnome/22.1.3/manjaro-gnome-22.1.3-minimal-230529-linux61.iso). 

The configuration consists of Shell commands, making it easy to install and customize without having to navigate through settings. Simply copy and paste the commands below. Please note that a part of the GitHub configuration requires actions to be performed on the GitHub website, which is not covered by the Shell commands provided here.

To ensure a smooth setup, I recommend starting with the tools from the [Utilities](#utilities) and [Installers](#installers) sections as they may be required for other parts of the configuration.

## Table of contents

<!-- TOC -->
* [Configuration for Manjaro 22.1.3 Gnome minimal](#configuration-for-manjaro-2213-gnome-minimal)
  * [Table of contents](#table-of-contents)
  * [Global](#global)
    * [Installers](#installers)
      * [pacman](#pacman)
      * [snap](#snap)
      * [AUR](#aur)
      * [Pamac](#pamac)
      * [pip](#pip)
      * [pipx](#pipx)
    * [System](#system)
    * [Text](#text)
      * [Spellcheckers](#spellcheckers)
      * [Fonts](#fonts)
  * [Gnome 4](#gnome-4)
    * [Extensions](#extensions)
      * [Blur my Shell](#blur-my-shell)
      * [Caffeine](#caffeine)
      * [Dash to Dock](#dash-to-dock)
      * [Disable unredirect fullscreen windows](#disable-unredirect-fullscreen-windows)
      * [Resource Monitor](#resource-monitor)
  * [Dev](#dev)
    * [Git](#git)
    * [GitHub](#github)
    * [Applications](#applications)
  * [Misc applications](#misc-applications)
    * [Social](#social)
    * [Graphisme](#graphisme)
    * [Utilities](#utilities)
<!-- TOC -->

## Global

### Installers

#### [pacman](https://wiki.archlinux.org/title/Pacman)

The package manager for [Arch Linux](https://archlinux.org/).

```sh
# selecting fastest mirror
sudo pacman-mirrors --fasttrack
# updating system
sudo pacman -Syu
```

#### [snap](https://ubuntu.com/core/services/guide/snaps-intro)

The official app store provided by [Canonical](https://canonical.com/), where developers can deploy their applications.

```sh
# install
sudo pacman -S snapd
sudo systemctl enable --now snapd.socket
# enable classic snap support
sudo ln -s /var/lib/snapd/snap /snap
# snap inside pamac
pamac install libpamac-snap-plugin
sudo sed -i 's/#EnableSnap/EnableSnap/g' /etc/pamac.conf
```

#### [AUR](https://wiki.archlinux.org/title/Arch_User_Repository)

Community-driven repository maintained for [Arch Linux](https://archlinux.org/).

```sh
# AUR inside pamac
sudo sed -i 's/#EnableAUR/EnableAUR/g' /etc/pamac.conf
sudo sed -i 's/#CheckAURUpdates/CheckAURUpdates/g' /etc/pamac.conf
```

#### [Pamac](https://wiki.manjaro.org/index.php/Pamac)

The package manager used in Manjaro Linux.

```sh
# disable icon when no update
sudo sed -i 's/#NoUpdateHideIcon/NoUpdateHideIcon/g' /etc/pamac.conf
# remove orphaned packages
sudo pamac remove -o
```

#### [pip](https://pypi.org/project/pip/)

Package installer for Python. Many applications rely on it, install it to use them.

```sh
python -m ensurepip --upgrade
```

#### [pipx](https://pypa.github.io/pipx/)

The recommended method for installing Python applications from pip. It provides the ability to install each application inside a separate isolated virtual environment, preventing any conflicts or interference with your system's Python environment. This approach helps keep your system clean and organized while managing Python applications.

```sh
python3 -m pip install --user pipx
python3 -m pipx ensurepath
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
sudo pacman -S aspell-en libmythes mythes-en languagetool
# french
sudo pacman -S aspell-fr mythes-fr
```

#### Fonts

```sh
# Emojis
sudo pacman -S noto-fonts-emoji
# Microsoft
sudo pamac build ttf-ms-win11-auto
# glacial indifference (a cool font)
wget https://www.fontsquirrel.com/fonts/download/glacial-indifference --output-document=glacial-indifference.zip
unzip glacial-indifference.zip -d glacial-indifference
font-manager --install glacial-indifference/*.otf
rm -r glacial-indifference.zip glacial-indifference
```

## [Gnome 4](https://www.gnome.org/)

### Extensions

```sh
# tool to install from cli
pipx install gnome-extensions-cli --system-site-packages 
```

#### [Blur my Shell](https://github.com/aunetx/blur-my-shell)

Add blur effect to Gnome!

```sh
gext install blur-my-shell@aunetx
dconf write /org/gnome/shell/extensions/blur-my-shell/panel/blur false
dconf write /org/gnome/shell/extensions/blur-my-shell/overview/style-components 3
```

#### [Caffeine](https://github.com/eonpatapon/gnome-shell-extension-caffeine)

To pause screen saving.

```sh
gext install caffeine@patapon.info
```

#### [Dash to Dock](https://micheleg.github.io/dash-to-dock/)

A nice dock.

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
dconf write /org/gtk/gtk4/settings/color-chooser/selected-color "(true, 0.0, 0.0, 0.0, 1.0)"
dconf write /org/gnome/shell/extensions/dash-to-dock/transparency-mode "'DYNAMIC'"
dconf write /org/gnome/shell/extensions/dash-to-dock/min-alpha 0
dconf write /org/gnome/shell/extensions/dash-to-dock/max-alpha 1
dconf write 
```

#### [Disable unredirect fullscreen windows](https://github.com/kazysmaster/gnome-shell-extension-disable-unredirect)

For glitches on fullscreen (e.g. with the dock not hiding).

```sh
gext install unredirect@vaina.lt
```

#### [Freon](https://github.com/UshakovVasilii/gnome-shell-extension-freon)

Display system temperatures (CPU, disk, video card), voltage and fan RPM. I use it to display the maximum temperature of the CPUs.

```sh
gext install freon@UshakovVasilii_Github.yahoo.com 
dconf write /org/gnome/shell/extensions/freon/hot-sensors "['__max__']"
dconf write /org/gnome/shell/extensions/freon/show-rotationrate false
dconf write /org/gnome/shell/extensions/freon/show-voltage false
dconf write /org/gnome/shell/extensions/freon/show-power false
dconf write /org/gnome/shell/extensions/freon/group-rotationrate false
dconf write /org/gnome/shell/extensions/freon/group-voltage false
```

#### [Gnome 4x UI Improvements](https://github.com/axxapy/gnome-ui-tune)

Offers small improvements on the Gnome overview, mainly bigger workspaces thumbnails and search box hidden when unused. 

```sh
gext install gnome-ui-tune@itstime.tech
```

#### [Resource Monitor](https://github.com/0ry0n/Resource_Monitor/)

Show some useful information about the system.

```sh
gext install Resource_Monitor@Ory0n
dconf write /com/github/Ory0n/Resource_Monitor/cpufrequencystatus false
dconf write /com/github/Ory0n/Resource_Monitor/decimalsstatus true
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

```sh
# visual extensions
gext install impatience@gfxmonk.net just-perfection-desktop@just-perfection panel-corners@aunetx rounded-window-corners@yilozt transparent-window-moving@noobsai.github.com
# useful extensions
gext install no-overview@fthx runcat@kolesnikov.se
```

## Dev

### Git

```
git config --global user.name "XXX"
git config --global user.email "XXX@XXX"
git config --global core.editor nano
```

### GitHub

```sh
ssh-keygen -t ed25519 -C "your-gh-email@something"
wl-copy < ~/.ssh/id_*.pub
```
Then add it [here](https://github.com/settings/ssh/new).


### Applications

```sh
# codium
sudo pacman -S code
# jetbrains toolbox
curl -fsSL https://raw.githubusercontent.com/nagygergo/jetbrains-toolbox-install/master/jetbrains-toolbox.sh | bash && /opt/jetbrains-toolbox/jetbrains-toolbox
```

## Misc applications

### Social

```sh
sudo pacman -S discord
```

### Graphisme

```sh
sudo pacman -S gimp
```


### Utilities

```sh
# allows to copy texts and images to clipboard in command line
sudo pacman -S wl-clipboard
# allows to manage fonts
sudo pacman -S font-manager
```


