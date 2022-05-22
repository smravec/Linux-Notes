# Arch on framework laptop fixes
```
sudo vim /etc/systemd/system.conf
```
find #RebootWathcdogSec and change it to following
```
RebootWatchdogSec=0
```

