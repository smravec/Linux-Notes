# Arch Linux Base install guide
#### Quick arch install guide


## Connect to internet (wifi)
start the iwctl tool 
```bash
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
.eg
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
.eg
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
mkswap dev/nvme0n1p2
swapon dev/nvme0n1p2
mkfs.ext4 dev/nvme0n1p3
```
# Install base
```
mount /dev/nvme0n1p3 /mnt
pacstrap /mnt base linux linux-firmware
genfstab -U /mnt >> /mnt/etc/fstab
```





