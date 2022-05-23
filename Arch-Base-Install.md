# Arch Linux Base install guide
#### Quick arch install guide
#### Before install
1. download arch iso and flash it onto usb stick with program called BalenaEtcher
2. plug your usb stick into you machine 
3. enter BIOS by pressing f2 when booting
4. go to boot settings and move your usb stick to the top of the load order (also if there is secure boot setting disable it)
5. save changes and exit bios

## Connect to internet (wifi)
start the iwctl tool 
```
iwctl
```
scan for networks
```
station wlan0 scan
```
show all available networks
```
station wlan0 get-networks
```
connect to network
```
station wlan0 connect NAME_OF_NETWORK
```

## Set up system clock and timezones
list all timezones (exit with q)
```
timedatectl list-timezones
```
set your timezone
```
ln -sf /usr/share/zoneinfo/REGION/CITY /etc/localtime
```
e.g.
```
ln -sf /usr/share/zoneinfo/Europe/Bratislava /etc/localtime
```
sync your clock
```
timedatectl set-ntp true
```
```
hwclock --systohc
```
## Partition your disk
list all available disks
```
fdisk -l
```
now start partitioning your disk (it could be named /dev/sda, /dev/nvme0n1 or /dev/mmcblk0, for the rest of this guide I will use /dev/nvme0n1)
```
fdisk YOUR_DISK
```
e.g.
```
fdisk /dev/nvme0n1
```
then view all the commands for fdisk
```
m
```
first create a new gpt table
```
g
```
then create 3 partitions (EFI,SWAP and MAIN)
### EFI (first create partition then assign the number 1 to it the select how big it should be then change the type to EFI partition)
```
n
1
(just press enter)
+550M
t
1
1
```
### SWAP (first create partition then assing the number 2 to it then select how big it should be then change the type to Linux swap)
```
n
2
(just press enter)
```
Now if using desktop pc set this to 5G if using laptop this should be at least your ram size + few gb (so if my ram is 32gb set this to +33G)
```
+YOUR_RAM_SIZE+FEWGB_OR_5G
```
.eg my ram size is 32gb
```
+33G
```
now change the type to Linux swap
```
t
2
```
i can get this number when typing L which shows all the available types
```
19
```
### Linux main filesystem (first create new partition then assign the number 3 to it then select how big it should be, you dont have to change the type because by default partitions are linux filesystems)
```
n
3
(just press enter)
(just press enter)
```
and finally to save all your changes press w
```
w
```
# Format partitions
format the EFI, SWAP and Linux file system partition
```
mkfs.fat -F32 /dev/nvme0n1p1
mkswap /dev/nvme0n1p2
swapon /dev/nvme0n1p2
mkfs.ext4 /dev/nvme0n1p3
```
## Install base
```
mount /dev/nvme0n1p3 /mnt
pacstrap /mnt base linux linux-firmware
genfstab -U /mnt >> /mnt/etc/fstab
```
## Chroot
```
arch-chroot /mnt
```
### Setup clock and timezone again
```
ln -sf /usr/share/zoneinfo/REGION/CITY /etc/localtime
hwclock --systohc 
```
### Download vim (basic vim commands: I to enter insert mode, Esc to exit insert mode, to exit and save :wq (also you have to be out of insert mode), to just exit without saving :q! (also you have to be out of insert mode))
```
pacman -S vim
```
### Setup for your keyboard layout
```
vim /etc/locale.gen
locale-gen
```
### Setup your hostname (name of the machine)
open /etc/hostname with vim
```
vim /etc/hostname
```
after that press I, write your hostname on the top , press esc and then press :wq
```
your_hostname_without_spaces_all_lowercap
```
e.g.
```
my_pc
```
open /etc/hosts with vim
```
vim /etc/hosts
```
copy or retype this into /etc/hosts
```
127.0.0.1   localhost
::1   localhost
127.0.1.1   your_hostname.localdomain  your_hostname
```
e.g.
```
127.0.0.1   localhost
::1   localhost
127.0.1.1   my_pc.localdomain  my_pc
```
### Setup root and user
setup root password
```
passwd 
```
add your user, set his password and give him permissions
```
useradd -m YOUR_USERNAME
passwd YOUR_USERNAME
usermod -aG wheel,audio,video,optical,storage YOUR_USERNAME
```
### Setup sudo
download sudo with pacman
```
pacman -S sudo
```
open sudo config with vim
```
EDITOR=vim visudo
```
find this line
```
#%wheel ALL=(ALL:ALL) ALL
```
press I and uncomment it so it looks like this
```
%wheel ALL=(ALL:ALL) ALL
```
save and exit by pressing Ecs and :wq

## Setup grub (bootloader)
download required packages
```
pacman -S grub efibootmgr dosfstools os-prober mtools
```
make EFI directory and mount your EFI partition there
```
mkdir /boot/EFI
mount /dev/nvme0n1p1 /boot/EFI
```
finnish setting up grub
```
grub-install --target=x86_64-efi  --bootloader-id=grub_uefi --recheck
grub-mkconfig -o /boot/grub/grub.cfg
```
## Last things before finnishing installation
install 
```
pacman -S base-devel network-manager
```
setup network manager
```
systemctl enable NetworkManager
```
## Reboot
exit chroot
```
exit
```
unmount your file system
```
umount -R /mnt
```
shutdown pc
```
shutdown now
```
after that you can remove you usb stick with iso and boot into your arch installation
