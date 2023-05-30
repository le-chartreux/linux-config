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
```

## Dev

### Git

```
git config --global user.name "XXX"
git config --global user.email "XXX@XXX"
git config --global core.editor nano
```

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


