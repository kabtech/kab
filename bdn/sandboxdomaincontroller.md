---
layout: kab
title: Deploy Sandbox Active Directory Domain Controller
group: bdn
---

### Sandbox Active Directory Domain Controller

I occasionally need one of these for evaluation or protopyping.

#### The Basics

- Spin up virtual machine and do clean install of Windows Server 2008 R2 (or whatever Windows Server version is appropriate for your project).
- Apply patches to get it current (often an epic test of your patience and determination).
- Do yourself a favor: snapshot your pristine server install so you can return to this happy place
- run `dcpromo` and follow wizard to conclusion
- restart server

#### If you need a self-signed cert to bind to LDAPS

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.

#### Add some fake users

I used the [RANDOM USER GENERATOR](https://randomuser.me/) API with the call below to get a comma delimited list of 20 users. 
```
https://randomuser.me/api/?results=20&nat=us&inc=name,email,&format=csv&noinfo
```

<br/>
<br/>
