---
layout: kab
group: ccc
title: VMware ESXi
---
### VMware ESXi

Control vm from shell:
```
vim-cmd vmsvc/getallvms
vim-cmd vmsvc/power.getstate <vmid>
vim-cmd vmsvc/power.on <vmid>
```

Use SCP client via Linux shell (including chronos) to retrieve file from esxi host
```
scp root@192.168.1.253:/vmfs/volumes/498bbb20-ccf6ac2d-4e2d-001517c46b24/Win7_01/Win7_01-flat.vmdk /home/chronos/user/Downloads/esxitemp/Win7_01-flat.vmdk
#expect to be challenged for the root password; ssh must be enabled on the esxi host
#NOTE: if you wish to transfer from one esxi host to another, you must edit firewall rules (under networking) to enable SSH client on the esxi host that will be acting as a client to the other to push the file:
scp /vmfs/volumes/blah/source_iso/Windows10pro.iso root@192.168.1.253:/vmfs/volumes/blah/source_software/
# you can test if the client can connect to the target (say 192.168.1.2) as follows (success message will be echoed back):
nc 192.168.1.2 22
```

Windows VM tuning guidance
```
#turn off vm logging in the vm config
#disable hibernation in guest
#disable system restore in guest
https://www.emc.com/collateral/software/white-papers/h8043-windows-virtual-desktop-view-wp.pdf
```

<br/>
<br/>
