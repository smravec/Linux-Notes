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
sudo pacman -S firefox
```
To enable hardware acceleration make sure that these settings in about:config are all set to true
```
media.ffmpeg.vaapi.enabled = true
media.navigator.mediadatadecoder_vpx_enabled = true
media.rdd-ffmpeg.enabled = true
```
also if using intel install
```
sudo pacman -S intel-media-driver
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
qemu (virtual machines)</br>
xcb-util-cursor (fixes cursor size in qtile)
```
sudo pacman -S cmatrix neofetch man-db man-pages libmagick krita xclip qemu xcb-util-cursor
```
