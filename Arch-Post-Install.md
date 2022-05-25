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
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```
### Display manager
```
yay -S ly
sudo systemctl enable ly.service
sudo systemctl disable getty@tty2.service
```
### Web browser
```
sudo pacman -S chromium
```
### Misc
```
yay -S acpi qeh kpcli alacritty
```
```
sudo pacman -S cmatrix neofetch man-db man-pages
```
