# Configuration for Manjaro 22.1.3 Gnome minimal

My personnal configuration for [Manjaro 22.1.3 minimal with Gnome 4 desktop](https://download.manjaro.org/gnome/22.1.3/manjaro-gnome-22.1.3-minimal-230529-linux61.iso).

I recommend that you setup the tools from the [Utilities](#utilities) and [Package managers](#package-managers) sections before the other parts, since they are sometimes needed.

## Global

### Package managers

#### Pacman

```sh
# selecting fastest mirror
sudo pacman-mirrors --fasttrack
# updating system
sudo pacman -Syu
```

#### Snap

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

#### AUR

```sh
# AUR inside pamac
sudo sed -i 's/#EnableAUR/EnableAUR/g' /etc/pamac.conf
sudo sed -i 's/#CheckAURUpdates/CheckAURUpdates/g' /etc/pamac.conf
```

#### Pamac

```sh
# disable icon when no update
sudo sed -i 's/#NoUpdateHideIcon/NoUpdateHideIcon/g' /etc/pamac.conf
# remove orphaned packages
sudo pamac remove -o
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

### Graphism

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


