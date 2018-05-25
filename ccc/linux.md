---
layout: kab
group: ccc
title: Linux Admin
---
### Linux admin goto commands

Add a user to a group
```
usermod -a -G examplegroup exampleusername
```
Create symbolic link to make an executable project start multiuser at boot
(Syntax order: item-pointed-to > symlink)
```
ln -s /etc/init.d/myproject /etc/rc2.d/S02myproject
* note that the 2 in rc2.d denotes multi user processes
#refer to 2nd answer here: https://unix.stackexchange.com/questions/20357/how-can-i-make-a-script-in-etc-init-d-start-at-boot
```

Setup a user to authenticate via ssh auth key:
```
https://wiki.centos.org/HowTos/Network/SecuringSSH#head-9c5717fe7f9bb26332c9d67571200f8c1e4324bc

Generate keypair using ssh-keygen.
If client is putty, you may need to import the private key into puttygen and save it in ppk format.
Merge the key into authorized_keys file in the .ssh subdirectory of the user's home folder on the target server.

```

`./<file or directory name>` indicates it is located in the current directory

Create a new user, set the password, and set the password to require change upon first logon:
```
useradd -c "Joe User" juser
passwd juser
passwd -e juser
```
grep stuff
```
grep -v "teststring" filename #returns all that do not contain the string
```

netstat equivalent of windows 'netstat -an'
```
netstat --tcp --numeric
```
Check disk usage
```
df -h
pvdisplay
fdisk -l
```
Find a file or directory somewhere down the subtree
```
find . -name 'ese*'
```
Copy all files from source to destination
```
cp -a /source/. /dest/
```
Get list of user accounts on server
```
cat /etc/passwd
```
Lookup a group by name or gid using the getent command:
```
getent group oinstall
getent group 500
#To show all the groups, just leave your search query off of the command:
getent group
```
Get redhat version
```
cat /etc/redhat-release
```
Use cifs mount to mount windows share
https://access.redhat.com/solutions/448263
```
mount -t cifs -o username=<share user>,password=<share password> //WIN_PC_IP/<share name> /mnt
mount -t cifs -o sec=ntlm,file_mode=0777‌​,dir_mode=0777,domain=aaa,username=bbb,password=zzzzzz //myserver/testshare$ /cifs01
mount -t cifs -o sec=ntlm,file_mode=0777‌​,dir_mode=0777,domain=dhp,credentials=/root/.cifs //dhpjumpbox/testshare$ /cifs01
... where /root/.cifs is a file that contains username=blah on 1st line and password=blah on 2nd line
to keep the credentials out of fstab, do this http://serverfault.com/questions/222074/fstab-and-cifs-mounting-possible-to-store-authentication-information-outside-of
```
Permissions/file creator/group the owner belongs to/
```
d~rwx~rws~r-x 5 infoprod informat 4096 Apr  2 20:45 navimedix
#The first column shows current permissions; it has ten slots. The first slot represents the type of file. 
#The remaining nine slots are actually three sets of permissions for three different categories of users. 
 -rw-rw-r-- 
#Those three sets are the owner of the file, the group in which the file belongs, and "others," meaning other users on the system. 
 -    (rw-)   (rw-)   (r--) 1 user user

servername:username:/dira/fubar> ls -l
total 8
drwxr-xr-x 4 username informat 4096 Apr  2 20:39 fudirectory
drwxrwsr-x 5 username informat 4096 Apr  2 20:45 bardirectory
||  |  |     |        |
||  |  |     |        group the owner belongs to
||  |  |     creator of the file or directory
||  |  permissions to everyone else on the system
||  permissions to the group in which the file belongs
|permissions to the owner of the file
type of object, where ‘d’ indicates directory

Legend for permissions:
r — file can be read 
w — file can be written to 
x — file can be executed (if it is a program) 
- (dash) — specific permission has not been assigned
s — for directory, means users may only remove files from directory if they have ownership of them (directly or via group)
```
Good reference on permissions:
https://www.linux.com/learn/understanding-linux-file-permissions
http://unix.stackexchange.com/questions/134332/precedence-of-user-and-group-owner-in-file-permissions

CHMOD Numbers Method
```
r (read) = 4 w (write) = 2 x (execute) = 1
#Numbers can be added together so you can specify read/write/execute permissions; read+write = 6, read+execute = 5, read+write+execute = 7
so for rw,rw,r
chmod 664 filename
```

/etc/shadow analysis
```
":" is the primary delimiter, with $ delimiting
username:$6$MblL.sn3$Pi4nVcl7pM3ivJDO8Tp8BEs5reEHf9bxfeFH8k6hTFlPthaa6IEFbmuOgzhX3b683pkJ57zH7aLxOlXswArJC0:16622:0:99999:7:::
1) Username
The first field is an easy one, it is the username of the particular account.
2) Password hashing details + hashed password
The most important string in the /etc/shadow file is definitely the second field. It includes the password details and consists of several parts:
$6 = SHA-512
$6Y/fI1nx$ = Salt and separators. The salt is a small string of characters to mix into the hashing function. Its goal is making it more difficult to perform certain password based attacks on the hashed password. This salt consists of characters a-z, A-Z, 0-9, / and .
Long string of characters = hashed password
The long string and its length depends on the hashing method used. With $6, or SHA-512, it will 86 characters.
Lengths:
- $1 = MD5 with 22 characters
- $5 = SHA-256 with 43 characters
Notes:
When the password field has a ! or *, then the account is locked. A double ! (!!) indicates a password has never been set.
3) Last changed
This number indicates when the password was last changed. The number does indicate the day number, starting from epoch date (1 January 1970). Right now that is in the 16000+ range.
4) Number of days before password can be changed
This field defines how long it takes before the password can be changed. In our case zero, so it can be changed now.
5) Number of days till required password change
Another pretty self-explanatory field, stating how long is left (in days), before a password change is required. A great option to force password changes.
6) Warning threshold in days
In line with previous field it describes the number of days till a warning will be giving. In this example it is a week.
7) Expire date
Also stored in days, describing when the account was expired (from epoch date).
8) Reserved field
Usually not used by Linux distributions
```
Restart server
```
shutdown -r now
```
Show all local file systems
```
cat /etc/fstab
```

List the running processes
```
ps -ef
```

Mount a vmdk
```
mount vmware-server-flat.vmdk /mnt/mntname/ -o ro,loop=/dev/loop1,offset=105906176 -t ntfs
```

<br/>
<br/>
