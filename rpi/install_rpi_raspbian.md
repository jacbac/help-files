Raspbian
========

Installation
------------

For official and updated documentation, go to http://elinux.org/RPi_Easy_SD_Card_Setup

First check the mount names of your SD card

```
df -h
```

For me it's often 'sdc1' for partition 1, 'sdc2' for partition 2, etc. but be carefull about that cause you maybe gonna wipe your entire HD ! And please read the doc and don't hesitate to do a 'man dd' before !

```
umount /dev/sdc1
umount /dev/sdc2
```

Once you have unmounted, [download the raspbian .img](http://www.raspberrypi.org/downloads), go to your download folder where the .img is, extract it, then (remember, that's the dangerous part)

```
sudo dd bs=4M if=RASPBIAN_IMAGE_NAME.img of=/dev/YOUR_DISK
```

In my case for the `2013-09-25-wheezy-raspbian` version,

```
sudo dd bs=4M if=2013-09-25-wheezy-raspbian.img of=/dev/sdc
```

Now, you can wait some times and take a break... The image is being 'loaded' to your lovely SD card !

To see the progress of the copy operation you can run in another terminal

```
sudo pkill -USR1 -n -x dd
```

The progress will be displayed (perhaps not immediately, due to buffering) in the original window, not the window with the pkill command.

At the end, you can read something like this

```
706+1 enregistrements lus
706+1 enregistrements écrits
2962227200 octets (3,0 GB) copiés, 284,085 s, 10,4 MB/s
```

Ensure the write cache is flushed and that it is safe to unmount your SD card

```
sudo sync
```

Remove SD card from card reader and plug-it in your raspberry :)


Raspi config
------------

First launch blabla,

1. Expand 
2. Set internationalisation options (locale, timezone, keyboard layout, etc.)
3.


SSH
---

Search the raspbian IP on private network (nmap needed)

```
nmap -sV --open 192.168.0.0/25 -p22
```

Note the raspbian IP then SSH it

```
ssh pi@{THE_RASPBIAN_IP}

login : pi
password : raspberry
```


Linux upgrade
-------------

```
sudo apt-get update
sudo apt-get upgrade
```


Install text-editor vim
-----------------------

```
sudo apt-get install vim
```


Update config.txt
-----------------

if needed, edit your general config file (for raspbian)

```
sudo vim /boot/config.txt
```

For my ol' TV set (connected with composite) replace default config by

```
# uncomment this if your display has a black border of unused pixels visible
# and your display can output without overscan
disable_overscan=0

# uncomment the following to adjust overscan. Use positive numbers if console
# goes off screen, and negative if there is too much border
overscan_left=32
overscan_right=16
overscan_top=-12
overscan_bottom=20

# uncomment to force a console size. By default it will be display's size minus
# overscan.
framebuffer_width=720
framebuffer_height=576

# uncomment for composite PAL
sdtv_mode=2

# Set stdv mode to 4:3 aspect ratio (default)
sdtv_aspect=1

#uncomment to overclock the arm. 700 MHz is the default.
arm_freq=800

# for more options see http://elinux.org/RPi_config.txt
core_freq=250
sdram_freq=400
over_voltage=0
gpu_mem=256

```


Add a new user
--------------

```
sudo adduser {USER_NAME}
```

Set it as a sudoer

```
sudo visudo
```

And then add (under pi):

```
{USER_NAME} ALL=(ALL) NOPASSWD: ALL
```

CTRL+O to save & CTRL+X to exit from nano editor (or CTRL+K then CTRL+X to save & exit from joe)

For dev purpose, add current user to www-data group

```
sudo adduser $LOGNAME www-data
```

Then exit & re-connect via ssh using {USER_NAME}

```
ssh {USER_NAME}@{THE_RASPBIAN_IP}
```

Change default password
-----------------------

login : pi
default password : raspberry

```
sudo passwd pi
```

Install usefull programs
------------------------

```
sudo apt-get install vim
```

Set up git (already installed with raspbian)

```
git config --global user.name "jacbac"
git config --global user.email "jacbachelier@gmail.com"
```

Configure bash, git, aliases...

```
vim .bashrc
vim .bash_aliases
vim .gitconfig
```


Install multimedia programs
---------------------------

```
sudo apt-get install vlc
```


Joystick
--------

Control X11 server with a joystick

```
sudo apt-get install xserver-xorg-input-joystick
```

It installs a default configuration file as `/usr/share/X11/xorg.conf.d/50-joystick.conf`, that is enough to provide features equivalent to a regular mouse.

But given the number of axes and buttons of my pad, it deserved a special configuration in `/etc/X11/xorg.conf.d/rumblepad.conf` :

look at `http://forum.ubuntu-fr.org/viewtopic.php?pid=947925`
```
Section "InputClass"
    Identifier  "Rumble Pad"
    Option      "MatchIsJoystick"   "on"
    Option      "MatchProduct"      "Logitech Logitech Rumble Pad"

    # Main stick axes: point
    Option      "MapAxis1"          "mode=relative axis=+1x deadzone=5000"
    Option      "MapAxis2"          "mode=relative axis=+1y deadzone=5000"

    # Second stick axes: scroll
    Option      "MapAxis3"          "mode=relative axis=+1zx deadzone=5000"
    Option      "MapAxis5"          "mode=relative axis=+1zy deadzone=5000"

    # Triggers: scroll vertically
    Option      "MapAxis4"          "mode=relative axis=+1zy deadzone=5000"

    # Directional pad: point
    Option      "MapAxis6"          "mode=accelerated axis=+1x deadzone=5000"
    Option      "MapAxis7"          "mode=accelerated axis=+1y deadzone=5000"

    # Buttons 1, 2 and 3 : click (no use for button 4)
    Option      "MapButton1"        "button=1"
    Option      "MapButton2"        "button=2"
    Option      "MapButton3"        "button=3"
    Option      "MapButton4"        "none"

    # Rear buttons: back and forward
    Option      "MapButton5"        "key=166"   # XF86Back
    Option      "MapButton6"        "key=167"   # XF86Forward

    # Triggers: no use
    Option      "MapButton7"        "none"
    Option      "MapButton8"        "none"

    # Special buttons
    Option      "MapButton9"        "key=135"   # select : Menu
    Option      "MapButton10"       "key=172"   # start : XF86AudioPlay
    Option      "MapButton13"       "key=180"   # home : XF86HomePage

    # Sticks click: click
    Option      "MapButton11"       "button=1"  # clic left stick
    Option      "MapButton12"       "button=3"  # clic right stick
EndSection
```

Usefull commands
----------------

Disk space usage overview

```
df -h
```
