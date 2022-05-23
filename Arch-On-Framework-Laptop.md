# Arch on framework laptop fixes
### Fix RebootWatchdogSec error message
```
sudo vim /etc/systemd/system.conf
```
find #RebootWatchdogSec and change it to following
```
RebootWatchdogSec=0
```
### Fix small font in grub
install ttf font
```
sudo pacman -S ttf-dejavu
```
generate grub font
```
sudo grub-mkfont -s 26 -o /boot/grub/grub_font.pf2 /usr/share/fonts/TTF/DejaVuSansMono.ttf
```
open grub config at /etc/default/grub
```
sudo vim /etc/default/grub
```
uncomment or add these lines to bottom
```
GRUB_FONT="/boot/grub/grub_font.pf2"
GRUB_GFXPAYLOAD_LINUX="keep"
```
save and exit
update the grub config
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
### Fix Xorg scaling
create and open .Xresources in ~/
```
vim ~/.Xresources
```
add this line
```
Xft.dpi: 192
```
<p> save and exit </p>
<p>update the xorg config</p>
```
xrdb -merge ~/.Xresources
```
