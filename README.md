# Configuration for Manjaro 22.1.3 Gnome minimal

## Global

### Pacman

#### Fastest mirror

```sh
// selecting fastest mirror
sudo pacman-mirrors --fasttrack

// updating system
sudo pacman -Syu
```

#### Remove orphaned packages

```sh
pacman -Qtdq | sudo pacman -Rns -
```

### System

```sh
// enabling TRIM (for better SSD performances)
sudo systemctl enable fstrim.timer
sudo systemctl start fstrim.timer
```

### Text

#### Spellcheckers

```sh
sudo pacman -S aspell-en libmythes mythes-en languagetool
// french
sudo pacman -S aspell-fr mythes-fr
```

#### Fonts

```sh
// Emojis
sudo pacman -S noto-fonts-emoji
// Microsoft
sudo pamac build ttf-ms-win11-auto
// manager
sudo pacman -S font-manager
// glacial indifference (a cool font)
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
sudo pacman -S code
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

### Utils

```sh
// allows to copy texts and images to clipboard in command line
sudo pacman -S wl-clipboard
```


