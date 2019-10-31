---
layout: kab
title: SMTP
group: ccc
---

### SMTP

Send email using python smtplib:
```
import smtplib
import email.utils
from email.mime.text import MIMEText

# Create the message
msg = MIMEText('This is the body of the message.')
msg['To'] = email.utils.formataddr(('Recipient', 'gern.blanston@gmail.com'))
msg['From'] = email.utils.formataddr(('Author', 'gern.blanston@fubar.com'))
msg['Subject'] = 'secdvlxpython01'

server = smtplib.SMTP('172.23.184.78', 443)
server.set_debuglevel(True) # show communication with the server
try:
    server.sendmail('gern.blanston@fubar.com', ['gern.blanston@gmail.com'], msg.as_string())
finally:
    server.quit()
```

Send email from any host with telnet installed:
```
# in shell, launch telnet session to server:
telnet servernameoripaddress smtp
>220 connection confirmation received from the server
# send server an EHLO with the domain name you wish to send as
EHLO fubar.com
>250 confirmation from server
# define sender address
MAIL FROM:blanston@fubar.com
>250 confirmation from server
# define the recipient address
RCPT TO:gern.blanston@gmail.com
>250 confirmation from server
# configure the mail subject and body
DATA (you signal end of data with a . on a line by itself)
>354 confirmation and instruction from server
Subject: yoursubjectlinecontent

youremailbodymessage
.
>250 confirmation of send from server


```



<br/>
<br/>
<br/>

