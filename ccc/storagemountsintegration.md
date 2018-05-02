---
layout: kab
group: ccc
title: Storage Mounts Integration
---

### Storage Mounts Integration

http://lifeofageekadmin.com/mount-access-nfs-exports-windows-server-2012-r2/
https://www.centos.org/docs/5/html/Deployment_Guide-en-US/s1-nfs-server-config-exports.html
https://unix.stackexchange.com/questions/116971/nfs-server-changes-in-etc-exports-file-need-service-restart
https://maprdocs.mapr.com/51/DevelopmentGuide/c-mounting-nfs-on-a-windows-client.html
http://blog.cuongnv.com/2009/11/windows-7-client-for-nfs-and-user-name.html

```
Use windows add/remove features to enable 'services for nfs' -- you want both 'administrative tools' and 'client'
Restart windows
Under administrative tools>services for network file system (NFS), select and right-click on 'services for nfs' and select 'properties'
For 'identity mapping source', check 'Active Directory domain name' and enter the fqdn domain name of where the AD user object resides
On the linux server you want to mount, lookup the corresponding user's UID and group ID (sudo cat /etc/passwd)
Using ADUC, edit the corresponding user object's uidNumber gidNumber to align with the linux user
Restart the windows computer
On the linux server, assure /etc/exports has been configured to share the desired location (after editing you will need to 'exportfs -ra' and if the server has never supported mounts before you may need to '/etc/init.d/nfs restart')
On the windows computer, you can map a drive as follows:
  servername:/mount/youcreated
```
<br/>
<br/>
