---
layout: kab
title: Atomic Pi basic Debian setup
group: bdn
---
### Atomic Pi basic Debian setup

I think of the Atomic Pi as a great value, but with an extremely touchy side. Some notes about the system itself:
- The CMOS reset button is way too easy to accidentally push when handling the board. DON'T, as it trashes any bootable eMMC partition you have created
- Must use POWERED USB hub. You will get erratic USB device behavior if you don't, including intermittent recognition of a bootable flash drive plugged into the hub.
- System power quirks: if you have the above powered USB hub attached and then switch off the primary system power, the system may remain running on the hub power.


Some about the Debian install:
```
#Install latest 'light' Debian from bootable USB flash drive
#If you want to install a desktop, wait to install it until after you have completed the initial system install
#Prep for additional installs
apt install update
#Install SSH server
apt install openssh-server
#Install sudo
apt install sudo
#Make user sudoer
usermod -aG sudo USERNAME

```
