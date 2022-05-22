# Arch Post install guide
## Connect to internet (wifi)
```
nmtui
```

## Sync pacman
```
sudo pacman -Syu
```

## Download packages
```
sudo pacman -S git
```

### Display manager
```
sudo pacman -S ly
sudo systemctl enable ly.service
sudo systemctl disable getty@tty2.service
```

### Desktop enviroment
```
sudo pacman -S xorg gnome
```

### Setup AUR
```
sudo git clone https://aur.archlinux.org/yay-git.git
cd yay
makepkg -si
```





