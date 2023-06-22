# backlight
backlight is a POSIX-compliant (pure bourne shell) script that allows you to get and set the brightness of the screen via /sys/backlight if supported by your system.
It also helps you set the permissions allowing a specific group to set the brightness.

See the examples folders for an example on how to use it to dim the screen when locking it, restoring the brightness when the screen is unlocked.

`% backlight --help`

__SYNOPSIS:__
    `backlight` [ `-g` | `--get` | `-get` ]
       Get the current brightness value in percent of MAX brightness.

    `backlight` [ `-s` | `--set` | `-set` ] percent
       Set the brightness to 'percent' of max brightness.  'percent' is an integer (anything trailing the first consecutive
       digits is ignored (e.g. a %-sign), allowing you to use the --get output as --set input without modification).

    `backlight` { `-i` | `--increase` | `-inc` } step
    `backlight` +step
       Increase the brightness by step percent units of max brightnes.$

    `backlight` { `-d` | `--decrease` | `-dec` } step
    `backlight` -step
       Increase the brightness by step percent units of max brightnes.

    `backlight` { `-o` | `--off` }
	Set the brightness to 0 (turnsthe backlight off).
       `--set` and `--increase` will never completely turn the brightness off, as it might have the consequence that when
       running `xset dpms force on` the brightness will unexpectedly be increased.


    `backlight --install` [ groupname ]
       Allow the specified group (or the video group if none specified) to set the brighness forth on.

       If systemd is in use '`backlight --install`' will also install, enable and run a systemd service making 'brightness'
       writeable by the specified group at system startup.

       '`backlight --install`' will replace the /etc/systemd/system/backlightgroup.service if it already exists.

       '`backlight --install`' must be executed with effective user-id 0 (run as root / with sudo).

__EXAMPLES:__
	Get current backlight brightness:
	`backlight --get`    

	Set backlight brightness to 75%:
	`backlight 75`	

	Increase backlight brightness with 5%-units:
	`backlight +5%`	 

	Decrease backlight brightness with 5%-units:
	`backlight -d 5`	  

	Flash the screen, restoring the backlight brightness afterwards:
	`B=$(backlight); backlight 0 ; sleep 0.5 ; backlight 100 ; sleep 0.5 backlight 0 ; sleep 0.5 ; backlight $B`     

__TODO:__ <br>
* Handle multiple backlight devices (right now it just picks the first one found)
