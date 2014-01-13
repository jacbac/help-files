XMBC Installation
=================

This conf was checked OK on an official and stable RaspBMC release writted on a 8Go Transend Class-10 SD-CARD.

* [RaspBMC Official](http://www.raspbmc.com/)
* [E-Linux official and updated documentation](http://elinux.org/RPi_Easy_SD_Card_Setup)


Install
-------

First check the mount names of your SD card

```
df -h
```

For me it's often 'sdc1' for partition 1, 'sdc2' for partition 2, etc. but be carefull about that cause you maybe gonna wipe your entire HD ! And please read the doc and don't hesitate to do a 'man dd' before !

```
umount /dev/sdc1
[umount /dev/sdc2]
```

Once you have unmounted, download the raspbmc .img [here](http://www.raspbmc.com/download/), go to your download folder where the .img is, extract it, then (remember, that's the dangerous part)

```
sudo dd bs=4M if=RASPBMC_IMAGE_NAME.img of=/dev/YOUR_DISK
```

In my case, i downloaded the sweet installer version called `installer.img`,

```
sudo dd bs=4M if=installer.img of=/dev/sdc
```

Now, you can wait some times and take a break... The image is being 'loaded' to your lovely SD card !

At the end, you can read something like this

```
150000+0 enregistrements lus
150000+0 enregistrements écrits
76800000 octets (77 MB) copiés, 29,2982 s, 2,6 MB/s
```

Ensure the write cache is flushed and that it is safe to unmount your SD card

```
sudo sync
```

Remove SD card from card reader and plug it in your Rpi :)

Plug also the RJ45 connector and your video connector (hdmi or s-video in my case).

Turn on the power of the Pi.

Raspbmc boots up, connects to the internet and over the next 20 minutes proceeds to download and install the root filesystem, kernel, bootloader, kernel modules and libraries.

It does all this automatically, reboots and installs XBMC.


SSH your rpi
------------

From a remote SSH client, find out where is the raspberry pi in the LAN (openssh server is enabled by default)

```
sudo nmap -sV --open 192.168.0.0/25 -p22
```

SSH on the raspi

```
ssh pi@[RASPBERRY.PI.IP]
```

Use default user 'pi' with password: 'raspberry'

The RaspBMC launch automaticaly the config process, so

* choose locale language
* choose timezone

User
----

Change the default password for the 'pi' user

```
sudo passwd pi
```

When asked, enter the new password twice

Create a new user

```
TODO
```

SSH Key
-------

From your desktop PC, generate new ssh-keys for raspi :

* [GitHub Help](https://help.github.com/articles/generating-ssh-keys)
* [French Help Git Attitude](http://www.git-attitude.fr/2010/09/13/comprendre-et-maitriser-les-cles-ssh/)

Copy your `.ssh/id_rsa.pub` local key on the raspi in a '.ssh/authorized_keys' file :

```
ssh-copy-id -i ~/.ssh/id_rsa.pub pi@[RASPBERRY.PI.IP]
```

Update repo
-----------

```
sudo apt-get update
```

DON'T launch a system upgrade (apt-get upgrade), XMBC will resolve this later


Program
-------

Install vim (or your prefered text-editor CLI friendly) for next update, install and config

```
sudo apt-get install vim
```

Install Git to get program/raspberry tweak with some usefull 'git clone' comand

```
sudo apt-get install git
```

WIP Install XboxDrv to get 

```
sudo apt-get install xboxdrv
```

Set your general config
-----------------------

Read some documented config files 

* [E-Linux Rpi Config](http://elinux.org/RPi_config.txt)
* [Evilpaul example config](https://raw.github.com/Evilpaul/RPi-config/master/config.txt)

Then edit if needed yours

```
sudo vim /boot/config.txt
```

For my ol' TV set (connected with composite) add

```
  # Set stdv mode to PAL (used in Europe)
  sdtv_mode=2
  # Set stdv mode to 4:3 aspect ratio (default)
  sdtv_aspect=1

  # Make display smaller to stop text spilling off the screen
  overscan_left=34
  overscan_right=0
  overscan_top=0
  overscan_bottom=24
```

Config on a launched RaspBMC
----------------------------

Restart the Raspberry and plug it to your TV screen

Choose your local language at the first launch

Configure audio for analog output (3.5mm jack)

System > Settings > Audio (note this may vary depending on the skin you are using)

  Select Analog as the Audio Output
  Choose analog (OMX) as your Audio output Device


[Optional] Set up a WiFi adapter
--------------------------------

```
@todo
```


[Optional] Mount on your destop PC your rasp file system
--------------------------------------------------------

Install if needed sshfs

```
sudo apt-get install sshfs
```

Then mount your rasp file system in a 'pi' temp folder, by example on /home/user_name/

```
sshfs login@server:/your_distant/mount_folder /your_local/mount_folder

mkdir pi
sshfs pi@192.168.0.10:/home/pi pi
```

The rasp file system is now accesible by nautilus or whatever GUI explorer.


[Optional] Configure a remote controller
----------------------------------------

WIP WIP WIP => Non-Working configuration : rumblePad seems to be recognize by rpi but not by xmbc version.

### Recognize your Logitech Rumble Pad II joystick

plug the USB dongle from the pad then 

```
lsusb
```

or more specificaly

```
lsusb -v -d 046d:c219

Bus 001 Device 004: ID 046d:c219 Logitech, Inc. Cordless RumblePad 2
xboxdrv --device-by-id 046d:c219 --type generic-usb --generic-usb-spec vid=046d,pid=c219,if=0,ep=2
```

### Overwriting the basic keymapping

XMBC comes with basic keymap definition for various controller. You can check them on

  https://github.com/xbmc/xbmc/tree/Eden/system/keymaps

Keymaps defined in user folders add to or override mappings in the global keymap

For Linux system

   $ HOME/.xbmc/userdata/

For example and for enhance your Logitech Rumble Pad II keymap definition, 

  http://wiki.xbmc.org/index.php?title=HOW-TO:Modify_keyboard.xml

Copy the original Logitech keymap to your userdata folder

  cp /opt/xbmc-bcm/xbmc-bin/share/xbmc/system/keymaps/joystick.Logitech.RumblePad.2.xml /home/pi/.xbmc/userdata/keymaps/

2) cp /opt/xbmc-bcm/xbmc-bin/share/xbmc/system/keymaps/keyboard.xml /home/pi/.xbmc/userdata/keymaps/

vim /home/pi/.xbmc/userdata/keymaps/keyboard.xml

Then go to your keymap directory and edit your keymap file

  cd /home/pi/.xbmc/userdata/keymaps/
  vim joystick.Logitech.RumblePad.2.xml

Example of enhanced keymapping

  http://pastebin.com/4z2SVJVm


[Optional] Games Emulators
--------------------------

WIP 

Nintendo 64
SNES


Help Notes
----------

### Basics

Start or stop XMBC

```
sudo initctl start xbmc
sudo initctl stop xbmc
```

Copying files to or from the Pi

```
scp /path/to/your_file.zip pi@[RASPBERRY.PI.IP]:~/path/to/your_new_copied_file_directory
```

### Logs

View active log

```
tail -F /home/pi/.xbmc/temp/xbmc.log
```

Copying a log file from the pi, to the current directory on your local machine

```
scp pi@[RASPBERRY.PI.IP]:/home/pi/.xbmc/temp/xbmc.log ./
```

