---
layout: kab
group: ccc
title: GitLab
---

### GitLab

#### Maintenance commands
```
#Get service status (location is /opt/gitlab/bin)
gitlab-ctl status
#Starting and stopping
gitlab-ctl start
gitlab-ctl stop
gitlab-ctl restart
#Tail process logs
See settings/logs.md

#Reconfiguring GitLab should occur in the event that something in its configuration (/etc/gitlab/gitlab.rb) has changed.
gitlab-ctl reconfigure

#refer to https://docs.gitlab.com/omnibus/maintenance/README.html
```

#### Strong cipher guidance -- up to qualys standards
```
https://github.com/cloudflare/sslconfig/blob/master/conf
EECDH+ECDSA+AESGCM:EECDH+aRSA+AESGCM:EECDH+ECDSA+SHA512:EECDH+ECDSA+SHA384:EECDH+ECDSA+SHA256:ECDH+AESGCM:ECDH+AES256:DH+AESGCM:DH+AES256:RSA+AESGCM:!aNULL:!eNULL:!LOW:!RC4:!3DES:!MD5:!EXP:!PSK:!SRP:!DSS

The configuration is defined in the file gitlab.rb
```

Location of config: /var/opt/gitlab/nginx/conf/nginx.conf

NOTE: for TLS/SSL, consumes cert and private key as separate base64 pem files.



<br/>
<br/>
