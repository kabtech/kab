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


