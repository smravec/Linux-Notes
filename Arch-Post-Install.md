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
acpi (cli battery status)</br>
feh (cli image viewer)</br>
kpcli (cli password manager)</br>
alacritty (terminal emulator)
```
yay -S acpi feh kpcli alacritty
```
cmatrix (cli animation)</br>
neofetch (os info)</br>
man-db and man-pages (manual about commands)</br>
libmagick (cli file conversion)</br>
krita (gui pixel art editor)</br>
xclip (clipboard for xorg)</br>
qemu (virtual machines)
```
sudo pacman -S cmatrix neofetch man-db man-pages libmagick krita xclip qemu
```
