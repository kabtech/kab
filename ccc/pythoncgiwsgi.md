---
layout: kab
group: ccc
title: Python CGI and WSGI
---

### Python CGI and WSGI

#### Show all CGI environment variables in Python:
```
import os
for name, value in os.environ.items():
    print(name, value)
    print("<br>")
```

#### Consume incoming html post values:
```
import cgi
form = cgi.FieldStorage()
for key in form.keys():
    strKey = str(key)
    print(strKey + ":<br/>")
    strValue = str(form.getvalue(strKey))
    print(strValue + "<br/>")
```



<br/>
<br/>
