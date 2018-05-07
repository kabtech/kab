---
layout: kab
group: ccc
title: Active Directory
---

### Active Directory

#### Approximation of 'disable' for an AD security groups

As a cautious first step before deleting an AD user object, you may be in the habit of disabling it for a period of time first. There is no equivalent for AD security groups, but there is a reasonable alternative:  
change the group type to 'Distribution'. Doing so leaves the group's SID and GUID in place, but eliminates the security authorization functionality of the group.



<br/>
<br/>
