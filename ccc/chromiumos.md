---
layout: kab
group: ccc
title: Chromium OS
---

### Chromium OS

Access the linux shell:
```
CTRL+ALT+T to open Crosh (Chrome OS Developer Shell)
type "shell" and press enter to enter into the shell environment
(the prompt will be chronos@localhost/$
With this user ID (chronos), you are allowed to sudo; the password is chrome.
```
Enable the keyboard backlight on a macbook air:
```
==SETTING THE KEYBOARD BRIGHTNESS===
https://neverware.zendesk.com/hc/en-us/community/posts/210539768-Macbook-Air-2011-works-great-backlit-keyboard-
Anyone can set the keyboard brightness in cloudready setting a value between 1 and 255 to this file (0 turns the lights off):  
/sys/devices/platform/applesmc.768/leds/smc\:\:kbd_backlight/brightness
For me the value 64 is pretty enough. So you can run the followed command into the shell (CTRL+ALT+T to open the Crosh - Chrome OS Developer Shell, type shell and press enter to enter into the shell environment - you can see the prompt 
chronos@localhost / $
waiting commands.
Run the followed command:
sudo sh -c 'echo 64 > /sys/devices/platform/applesmc.768/leds/smc\:\:kbd_backlight/brightness'
replacing 64 to any valud from 0 to 255 (0 turns off and 255 has maximum brightness). You can be required to type a password. Just type chrome and ENTER.
To check the current brightness, you can type this command (no password is required):
cat /sys/devices/platform/applesmc.768/leds/smc\:\:kbd_backlight/brightness
 With these informations, it is pretty easy to create python or shell scripts to increase or decrease the keyboard brightness. It's even possible to adjust the brightness according to the environment luminosity. The command bellow returns a tuple, where the first term varies from 0 to 255 according to environment luminosity.
cat /sys/devices/platform/applesmc.768/light
With this information one can make a script that, periodically, checks the environment and automatically decide if the backlight must be turned on or not.
```

Converting Chromebook firmware back to legacy BIOS  
https://mrchromebox.tech/#fwscript


Using crouton to chroot a different install of linux:
```
https://chriswells.io/blog/view/chromebook-for-power-users-part-2
```

Notes:
```
Please specify a username for the primary user: admin
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully

Here's some tips:

Audio from the chroot will now be forwarded to CRAS (Chromium OS audio server),
through an ALSA plugin.

Future Chromium OS upgrades may break compatibility with the installed version
of CRAS. Should this happen, simply update your chroot.

You can flip through your running chroot desktops and Chromium OS by hitting
Ctrl+Alt+Shift+Back and Ctrl+Alt+Shift+Forward.

You can start LXDE via the startlxde host command: sudo startlxde

You must install the Chromium OS extension for integration with crouton to work.
The extension is available here: https://goo.gl/OVQOEt

Unmounting /mnt/stateful_partition/crouton/chroots/jessie...
Done! You can enter the chroot using enter-chroot.
```

<br/>
<br/>

