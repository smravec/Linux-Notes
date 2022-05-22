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




