---
layout: kab
title: Atomic Pi basic Debian setup
group: bdn
---
### Atomic Pi basic Debian setup

I think of the Atomic Pi as a great value, but with an extremely touch side. Some notes about the system itself:
- The CMOS reset button is way to easy to accidentally push. DON'T
- Must use POWERED USB hub. You will get inconsistent USB device behavior if you don't, including no recognition of bootable flash drive.
- System power quirks: if you have the above powered USB hub attached and switch off the primary system power, the system may remain running.


Some steps after the install is completd:
```
#Install latest 'light' Debian from bootable USB flash drive
#If you want to install a desktop, wait to install it until after you have completed the initial system install
#Prep for additional installs
apt install update
#Install SSH
apt install openssh-server
#Install sudo
apt install sudo
#Make user sudoer
usermod -aG sudo USERNAME

```
