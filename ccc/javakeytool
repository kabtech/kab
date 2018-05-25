---
layout: kab
group: ccc
title: Java Keytool
---
### Java Keytool

NOTE: the Keystore password is used to verify keystore integrity, not confidentiality. When you access the keystore using the intended passphrase, the result output will indicate whether the store has been tampered with on the basis of that passphrase, but it will still provide the requested info.

When creating a new keystore with '-genkey', you are choosing to incorporate a private key into your keystore. In this case you will first be prompted for the keystore password, and then later, after you have provided the key attributes, you will be prompted for the private key password -- and it will offer to use the same password as the one you have already provided for the keystore. Since most people accept this default behavior, confusion may arise when using the key regarding for which purpose one is being asked for a password.


Generate certificate keystore with subject alternative name attributes:
```
keytool -genkey -alias fubar1.a.com -keyalg RSA -keysize 2048 -keystore fubar1.jks -ext SAN=dns:fubar1.a.com,dns:fubar1,dns:FUBAR1.A.COM,dns:FUBAR1
#NOTE must use the same -ext attribute when generating the CSR.
```

Create a new keytool-based truststore:
```
#import the certs as follows, command will wait for you to paste cert (standard input)
#-AND- it will also ask you to set a password the first time,
# and then supply the password on subsequent times
keytool -import -alias server1.fubar.com -keystore myTrustStore
keytool -import -alias server2.fubar.com -keystore myTrustStore
keytool -import -alias server3.fubar.com -keystore myTrustStore
```

The whole process of key creation, csr generation, cert request, and cert import into keystore:
```
keytool -genkey -alias fubar2.fubar.com -keyalg RSA -keysize 2048 -keystore fubar2.jks -ext SAN=dns:fubar2,dns:fubar2.fubar.com
keytool -certreq -alias fubar2.fubar.com -keyalg RSA -file fubar2.csr -keystore fubar2.jks -ext SAN=dns:fubar2,dns:fubar2.fubar.com
#if windows CA -- do this part on CA
certreq -submit -attrib "CertificateTemplate:DHPWebServer" fubar2.csr fubar2.cer
keytool -import -trustcacerts -alias fubar2.fubar.com -file fubar2.p7b -keystore fubar2.jks
```

<br/>
<br/>
