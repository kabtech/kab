---
layout: kab
group: ccc
title: GetSSL
---

### getssl Tool

This tool is for obtaining and renewing certificates from the letsencrypt public certificate authority (https://letsencrypt.org/), which employs the Automatic Certificate Management Environment (ACME) protocol. The certificates are free, but they are purposefully limited to a 90 day expiration window, so you have to manage certificate renewal accordingly. NOTE that getssl is just one of several ACME tools available for letsencrypt certificate management.

The repo:
https://github.com/srvrco/getssl

#### The command for cert renewal:
```
./getssl <FQDN of site>
```

#### Location of exe and config:
```
#config
/root/.getssl/<FQDN>/getssl.cfg
#exe
/root/getssl
```

#### Things that must be done to allow it to operate:
```
1. make sure site is listening on http on port 80 (only has to be locally, as getssl exe will be trying to reach it when running locally
2. make /etc/hosts entry pointing the FQDN to the loopback address
3. assure that the apache site .conf file has an alias defined for
   <FQDN>/.well-known/acme-challenge/
Note: if you can locally curl http://<FQDN>/.well-known/acme-challenge/<name of some test png file you place here>, then the getssl command should work too.
```

Remember you can test process against test letsencrypt server to avoid exceeding rate limit. When tests against this server succeed, then revise getssl.cfg to use prod server.



<br/>
<br/>
