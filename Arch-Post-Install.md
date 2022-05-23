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

### Window manager
```
sudo pacman -S xorg qtile
```
### Setup AUR
```
sudo git clone https://aur.archlinux.org/yay-git.git
cd yay
makepkg -si
```
### Display manager
```
yay -S ly
sudo systemctl enable ly.service
sudo systemctl disable getty@tty2.service
```
