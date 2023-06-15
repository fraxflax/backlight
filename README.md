# backlight
backlight is a POSIX-compliant (pure bourne shell) script that allows you to get and set the brightness via /sys/backlight

```backlight --help 

USAGE:
    backlight -get
    backlight { -set | -inc | -dec } percent
    backlight -install [ groupname ]

'backlight { -set | -inc | -dec }' requires
/sys/class/backlight/*/brightness to be writeable for the effective
user. Running backlight as root (e.g. via sudo) will obviously do it,
but better to make 'brightness' writeable for a group at boot time.

'backlight -install' will install, enable and run a systemd service
making 'brightness' writeable by the specified group, or for the video
group if none specified.

'backlight -install' will replace the
/etc/systemd/system/backlightgroup.service it if it already exists.

'backlight -install' must be run as root, requires your system to use
systemd and have systemctl in the $PATH.```

