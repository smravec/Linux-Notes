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
download acpi(cli battery status),feh (cli image viewer),kpcli(cli password manager),alacritty(terminal emulator)
```
yay -S acpi feh kpcli alacritty
```
download cmatrix(cli animation),neofetch(os info),man-db and man-pages(manual about commands)
```
sudo pacman -S cmatrix neofetch man-db man-pages
```
