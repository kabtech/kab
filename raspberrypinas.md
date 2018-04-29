---
layout: kab
title: Raspberry Pi NAS
group: bdn
---
### Raspberry Pi NAS Project

The project is to configure a RaspberryPi to act as a simple NAS server where the drives are external usb drives formatted exFAT. The PROs of this solution are 1) lower power consumption, 2) mobility of storage drives (simply power down the NAS and connect the drives to a computer running almost any OS), 3) minimal expense (you might already have 1 or more USB external drives, the Raspberry Pi is extremely inexpensive, and the software is free/open source). Among the CONs are low i/o performance. 

The Pi USB port connects to a powered 4-port USB hub, and the drives connect to the hub. The steps below are performed as root. The board is the Pi B-plus and the OS is Raspbian GNU/Linux 7 (wheezy).

The setup notes are as follows:
```
#list currently attached storage devices:
blkid

#obtain boot name of external drive's partition
fdisk -l

#add support for exfat:
apt-get install exfat-fuse

#create mount location:
cd /
mkdir extdsk01

#mount the drive manually
mount /dev/sda1 /extdsk01

#configure to mount automatically:
#run blkid to obtain the UUID of your drive
blkid
/dev/mmcblk0p1: SEC_TYPE="msdos" LABEL="boot" UUID="15CD-3B79" TYPE="vfat" 
/dev/mmcblk0p2: UUID="13d368bf-6dbf-4751-8ba1-88bed06bef77" TYPE="ext4" 
/dev/sda1: LABEL="1TB01" UUID="F0A5-981B" TYPE="exfat" 
#vi /etc/fstab to add the following line:
UUID=F0A5-981B /extdsk01 exfat defaults,auto,umask=000,users,rw 0 0

#install SAMBA
apt-get install samba samba-common-bin
#make a copy of the configuration file
cd /etc/samba
cp smb.conf smb.original
#edit smb.conf for our use case
#in the authentication section, uncomment the 'security = user' line
#at the very bottom of the file, add this section:
[NAS01]
comment = NAS01
path = /extdsk01
valid users = @users
force group = users
create mask = 0660
directory mask = 0771
read only = no

#add a user with which to connect to the share:
useradd NAS01 -m -G users
#and set the password for the above user

#add the above user for samba:
sudo smbpasswd -a NAS01 #you will be prompted for the password

#the share should now be reachable from your network

```

Use rsync to backup share to second disk:
```
#first time:
rsync -avhW --no-compress /mnt/extdsk02/photos /mnt/extdsk03/rsync/
#incremental:
rsync -avh --no-compress /mnt/extdsk02/photos /mnt/extdsk03/rsync/
```


Referenced the following:
- https://www.modmypi.com/blog/how-to-mount-an-external-hard-drive-on-the-raspberry-pi-raspian
- https://miqu.me/blog/2015/01/14/tip-exfat-hdd-with-raspberry-pi/
- https://miqu.me/blog/2015/04/14/exfat-with-raspberry-pi-continued/
- http://www.howtogeek.com/139433/how-to-turn-a-raspberry-pi-into-a-low-power-network-storage-device/

