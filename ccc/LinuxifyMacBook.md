---
layout: kab
group: ccc
title: Linuxify MacBook
---

### Linuxify MacBook

#### To start cooling fan sooner (system seems to run hot):
```
sudo add-apt-repository ppa:mactel-support
```

#### Disable touchpad during typing:
```
syndaemon -k -i 2 -d
```

#### Set keyboard back lighting to level of 64:
```
sh -c 'echo 64 > /sys/devices/platform/applesmc.768/leds/smc\:\:kbd_backlight/brightness'
```

#### Add support for brother printer scanner:
```
http://support.brother.com/g/b/downloadhowto.aspx?c=us&lang=en&prod=dcpl2540dw_us_as&os=128&dlid=dlf006893_000&flang=4&type3=625
```





<br/>
<br/>
