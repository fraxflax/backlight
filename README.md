# backlight

backlight is a POSIX shell script that allows you to get and set the brightness of the screen via /sys/backlight if supported by your system.
It also helps you set the permissions allowing a specific group to set the brightness.

See the examples folders for an example on how to use it to dim the screen when locking it, restoring the brightness when the screen is unlocked.

__SYNOPSIS:__

`backlight` [ OPTIONS ] [ `-g` | `--get` | `-get` ]  <br>
Get the current brightness value in percent of MAX brightness.  <br>

`backlight` [ OPTIONS ]  [ `-s` | `--set` | `-set` ] percent  <br>
Set the brightness to 'percent' of max brightness.  'percent' is an integer (anything trailing the first consecutive digits is ignored (e.g. a %-sign), allowing you to use the --get output as --set input without modification).

`backlight` [ OPTIONS ]  { `-i` | `--increase` | `-inc` } step  <br>
`backlight` +step  <br>
Increase the brightness by step percent units of max brightnes.

`backlight` [ OPTIONS ]  { `-d` | `--decrease` | `-dec` } step  <br>
`backlight` -step  <br>
Decrease the brightness by step percent units of max brightnes.

`backlight` [ OPTIONS ]  { `-o` | `--off` }  <br>
Set the brightness to 0 (turn the backlight off).  <br>
`-s` and `-d` will never completely turn the brightness off, as it might have the consequence that when running `xset dpms force on` the brightness will unexpectedly be increased.


`backlight --install` [ groupname ]  <br>
Allow the specified group (or the video group if none specified) to set the brighness forth on.

If udev is in use '`backlight --install`' will also install a udev rule making 'brightness' writeable by the specified group whenever a backlight device appears, so the permission survives reboots and hotplug.

The rule is written to /usr/local/lib/udev/rules.d/99-backlightgroup.rules and replaces any previous one. A file of the same name in /etc/udev/rules.d/ takes precedence over it, should a host need to differ.

Earlier versions installed a systemd service instead, which could not work reliably: the permission has to be set when the device appears, and no unit ordering expresses "after the graphics driver has probed". '`backlight --install`' removes that service if it is still present.

'`backlight --install`' must be executed with effective user-id 0 (run as root / with sudo).

__OPTIONS:__
`--sysfs` [ `first` | /sys/class/backlight/device | `all` ]

`backlight --sysfs first` ... <br>
Use the first device found in /sys/class/backlight/ . (This is the default.)

`backlight --sysfs /sys/class/backlight/intel_backlight` ... <br>
Use the specified backlight device, e.g. intel_backlight.

`backlight --sysfs all` ... <br>
Do the operation for all backlight devices found in /sys/class/backlight/ .

__EXAMPLES:__

Get current backlight brightness:  <br>
`backlight --get`    

Set backlight brightness to 75%:  <br>
`backlight 75`	

Increase backlight brightness with 5%-units:  <br>
`backlight +5%`	 

Decrease backlight brightness with 5%-units:  <br>
`backlight -d 5`	  

Turn screen off (set brightness to 0) for all backlight devices. <br>
`backlight --sysfs all --off`

Flash the screen, restoring the backlight brightness afterwards:  <br>
`B=$(backlight); backlight 0 ; sleep 0.5 ; backlight 100 ; sleep 0.5 ; backlight 0 ; sleep 0.5 ; backlight $B`     

