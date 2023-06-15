# backlight
backlight is a POSIX-compliant (pure bourne shell) script that allows you to get and set the brightness of the screen via /sys/backlight if supported by your system.
It also helps you set the permissions allowing a specific group to set the brightness.

See the examples folders for an example on how to use it to dim the screen when locking it, restoring the brightness when the screen is unlocked.

`% backlight --help`
```
USAGE:
    backlight [ -g | --get ]
       Get the current brightness value in percent of MAX brightness.

    backlight { -s | --set | -i | --increase | -d | --decrease } percent
       Set the brightness to 'percent' of max brightness or change it
       (increase / decrease) 'percent'. 'percent' is a integer with or
       without a trailing % sign.  Even though -s 0 will usually give
       a darker screen than -s 1, these options will never completely
       turn the brightness off as it might have unexpected
       consequences (see -off).

    backlight { -0 | -o | --off }
       Set the brightness to 0 (on some systems, 'xset dpms force off'
       also sets the brightness to 0 so it may make 'xset dpms force
       on' unexpectantly turn up the brightness under some
       circumstances).

    backlight --install [ groupname ]
       Allow the specified group (or the video group if none
       specified) to set the brighness forth on.

       Must be run by root.

       If systemd is in use 'backlight --install' will also install,
       enable and run a systemd service making 'brightness' writeable
       by the specified group at system startup.

       'backlight --install' will replace the
       /etc/systemd/system/backlightgroup.service it if it already exists.
```
TODO: <br>
* Handle multiple backlight devices (right now it just picks the first one found)
