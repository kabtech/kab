---
layout: kab
group: ccc
title: Raspbian OS
---
Default user object is pi.
Starting password is raspberry.
Required to sudo to run privileged commands.

Controlling external hard drive spin down:
```
#install hdparm or udisk (both this case):
apt-get -y update && apt-get -y install udisks hdparm
try sudo hdparm -S 10 /dev/sda -> spindown after 10*5 seconds.
or sudo udisks --set-spindown /dev/sda --spindown-timeout 20
replace /dev/sdawith your device.
```


<br/>
<br/>
