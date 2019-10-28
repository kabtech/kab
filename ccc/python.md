---
layout: kab
title: Python
group: ccc
---
### Python

#### Script for on-demand, throw-away https server
```
#Hit ctrl-C after you paste, at which point your populated array is ready for use.
$arrList = @();while (!$strStop){$arrList += read-host "Next entry:"}
#Or...use a construct like this if you want to be able to signal to a running script that you are done pasting entries:
$arrList = @();while ($arrList -notcontains "swordfish"){$arrList += read-host "Paste list or type 'swordfish' to indicate paste is done"}
```
# taken from http://www.piware.de/2011/01/creating-an-https-server-in-python/
# generate server.pem with the following command:
#    openssl req -new -x509 -keyout server.pem -out server.pem -days 365 -nodes
# run as follows:
#    python simple-https-server.py
# then in your browser, visit:
#    https://localhost:4443

import BaseHTTPServer, SimpleHTTPServer
import ssl

httpd = BaseHTTPServer.HTTPServer(('localhost', 4443), SimpleHTTPServer.SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket (httpd.socket, certfile='./server.pem', server_side=True)
httpd.serve_forever()
```
<br/>
<br/>
<br/>
