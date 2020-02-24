---
layout: kab
title: Python
group: ccc
---
### Python

#### Script for on-demand, throw-away https server
```
# taken from http://www.piware.de/2011/01/creating-an-https-server-in-python/
# and https://gist.github.com/dergachev/7028596
# generate server.pem with the following command:
#    openssl req -new -x509 -keyout server.pem -out server.pem -days 365 -nodes
# run as follows:
#    python yourscriptname.py
# then in your browser, visit:
#    https://localhost:4443 -or- https://hostipaddress:4443

import BaseHTTPServer, SimpleHTTPServer
import ssl

httpd = BaseHTTPServer.HTTPServer(('', 4443), SimpleHTTPServer.SimpleHTTPRequestHandler)
httpd.socket = ssl.wrap_socket (httpd.socket, certfile='./server.pem', server_side=True)
httpd.serve_forever()
```

#### Good discussion of byte-encoded strings:
```
https://stackoverflow.com/questions/6269765/what-does-the-b-character-do-in-front-of-a-string-literal
```

#### Create a listener on a particular port leveraging the sockets module (requires python 3.x):
```
# Echo server program
import socket

HOST = ''                 # Symbolic name meaning all available interfaces
PORT = 9999             # Arbitrary non-privileged port
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen(1)
    conn, addr = s.accept()
    with conn:
        print('Connected by', addr)
        while True:
            data = conn.recv(1024)
            if not data: break
            conn.sendall(data)
```

#### Create a caller to a particular port leveraging the sockets module (requires python 3.x):
```
# Echo client program
import socket

HOST = 'hostname'    # The remote host
PORT = 9999              # The same port as used by the server
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    s.sendall(b'Hello, world')
    data = s.recv(1024)
print('Received', repr(data))
```

#### Manual installation of additional version of Python:
```
#debian/ubuntu
apt-get install zlib1g-dev
#RHEL
yum install zlib
yum install zlib-devel
#get installer
wget http://www.python.org/ftp/python/3.3.3/Python-3.3.3.tar.xz
#decode XZ library
xz -d Python-3.3.3.tar.xz
#extract tar
tar -xvf Python-3.3.3.tar
#cd to extracted installer
cd Python-3.3.3 
# Start the configuration (setting the installation directory)
# By default files are installed in /usr/local.   
./configure
#build (compile) the source and
#perform an alternate install -- so as not to replace existing python
make && make altinstall
#update PATH variable to include new python version
export PATH="/usr/local/bin/python3.3:$PATH"
#install python 'six' library:
wget library from pypi
cd six-1.10.0
python3.3 setup.py install
#appdirs
wget https://pypi.python.org/packages/48/69/d87c60746b393309ca30761f8e2b49473d43450b150cb08f3c6df5c11be5/appdirs-1.4.3.tar.gz
cd appdirs-1.4.3
python3.3 setup.py install
#pyparsing
wget https://pypi.python.org/packages/3c/ec/a94f8cf7274ea60b5413df054f82a8980523efd712ec55a59e7c3357cf7c/pyparsing-2.2.0.tar.gz
cd pyparsing-2.2.0
python3.3 setup.py install
#packaging
wget https://pypi.python.org/packages/c6/70/bb32913de251017e266c5114d0a645f262fb10ebc9bf6de894966d124e35/packaging-16.8.tar.gz
cd packaging-16.8
python3.3 setup.py install
#et_xmlfile
wget https://pypi.python.org/packages/22/28/a99c42aea746e18382ad9fb36f64c1c1f04216f41797f2f0fa567da11388/et_xmlfile-1.0.1.tar.gz
cd et_xmlfile-1.0.1
#jdcal
wget https://pypi.python.org/packages/9b/fa/40beb2aa43a13f740dd5be367a10a03270043787833409c61b79e69f1dfd/jdcal-1.3.tar.gz
cd jdcal-1.3
python3.3 setup.py install
#install setuptools
cd setuptools-35.0.2
python3.3 setup.py install
#openpyxl
wget ....
cd openpyxl-2.4.7
python3.3 setup.py install
```




<br/>
<br/>
<br/>
