---
layout: kab
title: GNU gpg
group: ccc
---

### GNU gpg

#### Generate keyfile in a particular location
```
gpg --homedir /home/fubar/gpgkeytest --gen-key
# A dialog will walk you through the remaining inputs 
#If the process seems to hang during the 'gaining entropy phase', open another shell and run this command until the process completes:
dd if=/dev/sda of=/dev/zero
#(this command reads from your hard drive and discards the output, because writing to /dev/zero will does nothing.)
```
#### List all keys in the keystore:
```
gpg -v --list-keys
```

#### List all components of a particular key (including subkey IDs):
```
gpg --edit-key "84840EA6B62C743BDC4108EAF939BDEF01DCCF89"
```

#### Dump the key certificate to screen:
```
gpg -a --export "keyid" | gpg --list-packets --verbose
```

#### Export public and private keys:
```
#public
gpg -a --export <keyid>
#private
gpg --export-secret-key -a <keyid>
```

#### NOTE that gpg is capable of supporting symmetric encryption:
```
#use the --symmetric switch as follows:
gpg --symmetric plaintextfile.txt
#you will be prompted twice for the passphrase that will be used for the symmetric cipher
#person who wishes to decrypt will be challenged for the passphrase

#method to encrypt pipeline input to a file
#you will be prompted for the symmetric passphrase
echo "heron"|gpg2 --symmetric -o /home/fubar/e.enc
#doesn't work on RHEL7. I have to encrypt from a file or i don't get the passphrase prompt
```

#### Excellent reference on gpg keys:
```
https://davesteele.github.io/gpg/2014/09/20/anatomy-of-a-gpg-key/
see also https://tools.ietf.org/html/rfc4880
```



<br/>
<br/>
<br/>
