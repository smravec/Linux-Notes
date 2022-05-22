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

```
timedatectl list-timezones
```
```
ln -sf /usr/share/zoneinfo/REGION/CITY /etc/localtime
```
.eg
```
ln -sf /usr/share/zoneinfo/Europe/Bratislava /etc/localtime
```
```
timedatectl set-ntp true
```
```
hwclock --systohc
```
