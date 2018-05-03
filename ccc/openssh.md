---
layout: kab
title: OpenSSH
group: ccc
---

### OpenSSH

NOTE: The server can be configured for just key based authentication OR for key and password both. The latter is less common and is generally used in 2 factor authentication scenarios.

If installed on Win7, executables will likely be located at 'C:\Program Files (x86)\OpenSSH\bin'; open the command shell, navigate to the bin directory and run desired exe's.

Show a server's host key fingerprint:
```
ssh-keygen -E md5 -lf <(ssh-keyscan hostname 2>/dev/null)
#the -E is used to specify the hash algorithm
```

Generate new key, where you will be asked for filename. will be written to openssh bin directory and both the private and public key will be created, where the public key will have a .pub extension
```
ssh-keygen -t rsa -b 2048 -C "keyname" -N c048abd94184ef9172f8fe507b06de65
```
Convert source openssh public key file kab3.pub to IETF SECSH format. conversion will be printed to screen and will need to be pasted into text file. Note that you do not have to keep the  comment section of the key.

```
ssh-keygen.exe -e -f kab3.pub
```
If the key is generated with a passphrase, the passphrase will be requested by the client when you go to login

List the fingerprint of a previously-generated private or public key:
```
#to use md5 for the hashing function:
ssh-keygen -E md5 -lf keyfilepath
#to use the installed ssh-keygen default for the hashing function:
ssh-keygen -lf keyfilepath
#to use sha1 as the hashing function:
ssh-keygen -E sha1 -lf keyfilepath
```



Regarding RoboFTP SSH key support

The key export function exports keys in the openSSH format * in many cases you will need to export to IETF format to make importable

https://wiki.archlinux.org/index.php/SSH_Keys SSH keys always come in pairs, one private and the other public. The private key is known only to you and it should be safely guarded. By contrast, the public key can be shared freely with any SSH server to which you would like to connect.

When an SSH server has your public key on file and sees you requesting a connection, it uses your public key to construct and send you a challenge. This challenge is like a coded message and it must be met with the appropriate response before the server will grant you access. What makes this coded message particularly secure is that it can only be understood by someone with the private key. While the public key can be used to encrypt the message, it cannot be used to decrypt that very same message. Only you, the holder of the private key, will be able to correctly understand the challenge and produce the correct response.

This challenge-response phase happens behind the scenes and is invisible to the user. As long as you hold the private key, which is typically stored in the ~/.ssh/ directory, your SSH client should be able to reply with the appropriate response to the server.

Because private keys are considered sensitive information, they are often stored on disk in an encrypted form. In this case, when the private key is required, a passphrase must first be entered in order to decrypt it. While this might superficially appear the same as entering a login password on the SSH server, it is only used to decrypt the private key on the local system. This passphrase is not, and should not, be transmitted over the network.


<br/>
<br/>
<br/>
