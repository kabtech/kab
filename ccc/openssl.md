---
layout: kab
group: ccc
title: OpenSSL
---

Generate new keystore and a corresponding certificate signing request:
```
openssl req -newkey rsa:2048 -keyout yourname.key -out yourname.csr
#depending on the default of your openssl, you may have to use the following to suppress des3 encryption of the private key
openssl req -nodes -newkey rsa:2048 -keyout yourname.key -out yourname.csr
```

Create a new keystore -- with passphrase -- and csr including SAN using a conf file:
```
#Create conf file in this format:
[ req ]
default_bits = 2048
prompt = no
encrypt_key = no
default_md = sha256
distinguished_name = dn
req_extensions = req_ext
 
[ dn ]
CN = fubar.com
emailAddress = ssl@fubar.com
O = Example Company
OU = Example Unit
L = City
ST = State
C = US
 
[ req_ext ]
subjectAltName = DNS: fubar.com, DNS: fubar.net, DNS: fubar.biz

#process request as follows: 
openssl req -new -passout pass:"Pomegranate" -nodes -newkey rsa:2048 -config fubar_com.conf -keyout fubar_com.key -out fubar_com.csr

```

Remove passphrase from a passphrase protected key (you will be challenged for the passphrase):

```
openssl rsa -in www.key -out new.key
```
Retrieve certificate chain presented by a site:
```
openssl s_client -starttls ftp -showcerts -connect fubar1.fubar.com:21 #where -starttls protocol is limited to smtp, pop3, imap, ftp, and xmpp

#otherwise just:
openssl s_client -showcerts -host fubar1.fubar.com -port 636

#or:
openssl s_client -showcerts -connect fubarserver:5250

#if you specifically need to retrieve the cert's expiration date:
openssl s_client -showcerts -connect fubarserver:5250 2>/dev/null | openssl x509 -noout -dates

#if you need to display full cert info:
openssl s_client -showcerts -connect fubarserver:5250 2>/dev/null | openssl x509 -text

```

Just send the text-based details of a given base64 encoded certificate file to the screen:
```
openssl x509 -in fubar.cer -noout -text
```

Certbot manual guidance
```
https://community.letsencrypt.org/t/question-about-correct-way-to-obtain-certificate-using-certonly/20726
```

Combine key and pem files into a pkcs12 (pfx/p12) file (can include certs in chain, or you can purposefully omit)
```
openssl pkcs12 -export -out fubar.p12 -inkey fubar.key -in fubar_com.pem -certfile DigiCert_SHA2_Secure_Server_CA.pem -certfile DigiCert_Global_Root_CA.pem
```

Extracting Certificate and Private Key Files from a .pfx File
```
Run the following command to export the private key: 
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes

Run the following command to export the certificate: 
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem

Run the following command to remove the passphrase from the private key: 
openssl rsa -in key.pem -out server.key
```

Transform .pfx file generated and exported from mmc to separate private key and certificate pem files that can be used by gitlab:
```
#use mmc to create cert, being sure to set it to allow private key export (results in .pfx file)
#transport .pfx file to linux server
#extract just the certificate:
openssl pkcs12 -clcerts -nokeys -in "YourPKCSFile" -out certificate.crt (you will be prompted for key password)
#extract just the CA certificate:
openssl pkcs12 -cacerts -nokeys -in "YourPKCSFile" -out ca-cert.ca
#extract the private key in password protected format:
openssl pkcs12 -nocerts -in "YourPKCSFile" -out private.key
#remove the passphrase:
openssl rsa -in private.key -out "NewKeyFile.key"

#adapted from to https://serverfault.com/questions/515833/how-to-remove-private-key-password-from-pkcs12-container

```

