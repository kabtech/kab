---
layout: kab
group: ccc
title: Lubuntu Desktop
---

### Lubuntu Desktop (LXDE desktop on Ubuntu)

#### Use OpenConnect in lieu of Cisco AnyConnect:
```
sudo apt-get install network-manager-openconnect-gnome

#This adds an option to Network Connections. When you choose to add a connection, there'll be a new option under VPN Connections to add a "Cisco AnyConnect Compatible VPN (openconnect)". You can then connect to the VPN through the networks applet (in the system tray).
#http://askubuntu.com/questions/154699/how-do-i-install-the-cisco-anyconnect-vpn-client
```

#### Install and configure the Citrix ICA Web Client:
```
https://help.ubuntu.com/community/CitrixICAClientHowTo
```

#### Install Oracle java:
```
http://ubuntuhandbook.org/index.php/2014/02/install-oracle-java-6-7-or-8-ubuntu-14-04/
```

#### UInstall Eclipse:
```
http://ubuntuhandbook.org/index.php/2016/01/how-to-install-the-latest-eclipse-in-ubuntu-16-04-15-10/
```

#### Add entries to start menu:
```
Location: /home/userdir/.local/share/applications
File: create .desktop file
https://help.ubuntu.com/community/Lubuntu/Windows#How_to_make.2Fadd_an_application_to_the_.22start.22_menu.
```

#### Shrink Synaptics touch pad area to virtually nothing:
```
#first find device id
xinput list
#then shrink area for device
xinput set-prop "deviceID" "Synaptics Area" 1, 1, 1, 1
#related info: https://stevenkohlmeyer.com/fixing-palm-detect-ubuntu-14-04/
```

#### Install VMware Horizon View
```
Obtain installer from VMware
Installed libpng12-0_1.2.54-1ubuntu1_amd64.deb from https://packages.ubuntu.com/xenial/amd64/libpng12-0/download
cp /usr/lib/x86_64-linux-gnu/libpng12.so.0 /usr/lib/vmware/libpng12.so.0
(to correct error: vmware-remotemks-container: /usr/lib/vmware/libpng12.so.0: version `PNG12_0' not found (required by vmware-remotemks-container))
```



<br/>
<br/>
