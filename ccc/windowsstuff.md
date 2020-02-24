---
layout: kab
group: ccc
title: Windows OS Stuff
---

### Windows OS Stuff

#### WMI queries
```
#return essential server info:
wmic /node:citpfile05.fubar.local cpu get name, caption, maxclockspeed, systemname
#return local storage info:
wmic logicaldisk get size,freespace,caption
```

#### Clear slack space on drive or path:
```
cipher /w:D:\somefolder
```

#### Correct for font size issues with Quicken on macbook running Windows10:
```
https://www.quicken.com/support/menu-quicken-missing-not-working-appears-doubled-or-font-size-too-large-or-small
Right-click the Quicken icon on your desktop and select Open file location.
Right-click the qw.exe file and select Properties.
Select the Compatibility tab.
Check the box for 'Override high scaling behavior' and set the 'Scaling performed by' to Application.
```

#### Use NFS mount via Windows7 Enterprise edition:
```
#refer to https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh509016(v=ws.10)
https://unix.stackexchange.com/questions/116971/nfs-server-changes-in-etc-exports-file-need-service-restart
https://maprdocs.mapr.com/51/DevelopmentGuide/c-mounting-nfs-on-a-windows-client.html
http://blog.cuongnv.com/2009/11/windows-7-client-for-nfs-and-user-name.html

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

#### Set environment variable to persist through current session
```
set zquantum=blah~blah
```

#### Configure Windows 2012 Server remote desktop session host to consume the services of a license server:
```
#https://www.tbngconsulting.com/blog/bid/404182/Licensing-mode-for-the-Remote-Desktop-Session-Host-is-not-configured
$obj = gwmi -namespace "Root/CIMV2/TerminalServices" Win32_TerminalServiceSetting
$obj.SetSpecifiedLicenseServerList("server1.fubar.com")
HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\RCM\Licensing Core\LicensingMode
You need to change the DWORD to 2 for Per Device or 4 for Per User.
```

<br/>
<br/>
