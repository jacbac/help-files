XMBC Installation
=================

This conf was checked OK on a distro writted on a 8Go Transend Class-10 SD-CARD with a Wifi dongle: ...

Easy detailed SD Card setup :

* http://www.raspbmc.com/wiki/user/os-x-linux-installation/
* http://www.raspbmc.com/wiki/user/windows-installation/

EDIT : 

Just to say, if you use the raspBMC installer, you have the option to input the wireless network settings prior to imaging the disk. Once booted you can use SSH to sort out turning on the web service for the android remote control.
Doing this I was able to set up raspBMC without a mouse, keyboard or ethernet cable.

Plug the RJ45 connector (wifi conf is setted up later in this file).

Turn on the power of the Pi.

Raspbmc boots up, connects to the internet and over the next 20 minutes proceeds to download and install the root filesystem, kernel, bootloader, kernel modules and libraries.

It does all this automatically, reboots and installs XBMC.

From a remote SSH client, find out where is the raspberry pi in the LAN (openssh server is enabled by default)

    sudo nmap -sV --open 192.168.0.0/25 -p22

SSH on the raspi

    ssh pi@[RASPBERRY.PI.IP]

Use default user 'pi' with password: 'raspberry'

The RaspBMC launch automaticaly the config process, so

* choose locale language
* choose timezone

DON'T launch a system upgrade (apt-get upgrade), XMBC will resolve this later => or prepare to trash your fresh cloned distrib RaspBMC :(
DON'T try to install Tight VNC Server => idem

User
----

Change the default password for the 'pi' user

  sudo passwd pi

When asked, enter the new password twice

Create a new user
... TODO


SSH Key
-------

From your desktop PC, generate new ssh-keys for raspi : https://help.github.com/articles/generating-ssh-keys
More info [FR]: http://www.git-attitude.fr/2010/09/13/comprendre-et-maitriser-les-cles-ssh/

Copy your '.ssh/id_rsa.pub' local key on the raspi in a '.ssh/authorized_keys' file :

  ssh-copy-id -i ~/.ssh/id_rsa.pub pi@[RASPBERRY.PI.IP]

Update repo
-----------

  sudo apt-get update

DON'T launch a system upgrade (apt-get upgrade), XMBC will resolve this later

Program
-------

Install vim (or your prefered text-editor CLI friendly) for next update, install and config

  sudo apt-get install vim

Install Git to get program/raspberry tweak with some 'git clone' comand

  sudo apt-get install git

WIP Install XboxDrv to get 

  sudo apt-get install xboxdrv

[Optional] Mount on your destop PC your rasp file system
-------------------------------------------------------

Install if needed sshfs

  sudo apt-get install sshfs

sshfs login@server:/your_distant/mount_folder /your_local/mount_folder

Then mount your rasp file system in a 'pi' temp folder, by example on /home/user_name/

  mkdir pi
  sshfs pi@192.168.0.10:/home/pi pi

The rasp file system is now accesible by nautilus or whatever GUI explorer.

Set your general config
-----------------------

Read some documented config files 

  http://elinux.org/RPi_config.txt
  https://raw.github.com/Evilpaul/RPi-config/master/config.txt

Then edit if needed yours

  sudo vim /boot/config.txt

For my ol' TV set (connected with composite) add

  # Set stdv mode to PAL (used in Europe)
  sdtv_mode=2
  # Set stdv mode to 4:3 aspect ratio (default)
  sdtv_aspect=1

  # Make display smaller to stop text spilling off the screen
  overscan_left=34
  overscan_right=0
  overscan_top=0
  overscan_bottom=24

Config on a launched RaspBMC
----------------------------

Restart the Raspberry and plug it to your TV screen

Choose your local language at the first launch

Configure audio for analog output (3.5mm jack)

System > Settings > Audio (note this may vary depending on the skin you are using)

  Select Analog as the Audio Output
  Choose analog (OMX) as your Audio output Device

Set up a WiFi adapter
---------------------

WIP


[Optional] Configure a remote controller
----------------------------------------

WIP

### Recognize your Logitech Rumble Pad II joystick

plug the USB dongle from the pad then 

  lsusb

or more specificaly

  lsusb -v -d 046d:c219

Bus 001 Device 004: ID 046d:c219 Logitech, Inc. Cordless RumblePad 2

  xboxdrv --device-by-id 046d:c219 --type generic-usb --generic-usb-spec vid=046d,pid=c219,if=0,ep=2

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

Games Emulators
---------------

WIP 

Nintendo 64
SNES

Help Notes
---------

### Basics

Start or stop XMBC

  sudo initctl start xbmc
  sudo initctl stop xbmc

Copying files to or from the Pi

  scp /path/to/your_file.zip pi@[RASPBERRY.PI.IP]:~/path/to/your_new_copied_file_directory

### Logs

View active log

  tail -F /home/pi/.xbmc/temp/xbmc.log

Copying a log file from the pi, to the current directory on your local machine

  scp pi@[RASPBERRY.PI.IP]:/home/pi/.xbmc/temp/xbmc.log ./


