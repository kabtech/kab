---
layout: kab
group: ccc
title: Active Directory
---

### Active Directory

#### Approximation of 'disable' for an AD security groups

As a cautious first step before deleting an AD user object, you may be in the habit of disabling it for a period of time first. There is no equivalent for AD security groups, but there is a reasonable alternative:  
change the group type to 'Distribution'. Doing so leaves the group's SID and GUID in place, but eliminates the security authorization functionality of the group.

#### Use dsacls to modify permission of one user to one attribute
```
# here we are giving the user auth to change his own gidNumber attribute
dsacls "\\beta.fubar.com\CN=Blanston\, Gern,OU=Test,OU=BetaUsers,OU=_Beta,DC=beta,DC=fubar,DC=com" /G beta\gblanston:RPWP;gidNumber;
```

#### Configure granular delegation to allow a user to perform replication synchronization
https://social.technet.microsoft.com/wiki/contents/articles/21565.active-directory-delegate-replication-rights-to-non-admins.aspx


<br/>
<br/>
