---
layout: kab
group: ccc
title: Okta IDP
---

### Okta Cloud Identity Provider

#### Active Directory Integration

Tested agent rev: 3.4.12.0

Given the following conditions:
- JIT Provisioning / Create and update users on login: checked
- Schedule import: set to never 
- Do not import users: checked
- New users
    - Auto-confirm new users: checked
    - Auto-activate new users: checked
    
When a user attempts login with a userID that matches 'MATCH SETTINGS', JIT creates and makes active the Okta user object.


<br/>
<br/>
