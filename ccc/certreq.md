---
layout: kab
group: ccc
title: Windows CertReq
---

### Windows CertReq Command Line

#### Basic command for requesting cert when in possession of a CSR file:
```
certreq -submit -attrib "CertificateTemplate:FubarWebServer" mynewcsr.csr myserver.cer
#Must reference an existing template
#Depending on your auth and CA config, your request may land in a queue pending approval.
```


<br/>
<br/>
