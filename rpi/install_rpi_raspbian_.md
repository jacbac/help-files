Raspbian
========

Installation
------------

For official and updated documentation, go to http://elinux.org/RPi_Easy_SD_Card_Setup

First check the mount names of your SD card

> df -h

For me it's often 'sdc1' for partition 1, 'sdc2' for partition 2, etc. but be carefull about that cause you maybe gonna wipe your entire HD ! And please read the doc and don't hesitate to do a 'man dd' before !

> umount /dev/sdc1
> umount /dev/sdc2

Once you have unmounted, download the raspbian .img at http://www.raspberrypi.org/downloads, go to your download folder where the .img is, extract it, then (remember, that's the dangerous part)

> sudo dd bs=4M if=RASPBIAN_IMAGE_NAME.img of=/dev/YOUR_DISK

In my case for the 2013-09-25-wheezy-raspbian,

> sudo dd bs=4M if=2013-09-25-wheezy-raspbian.img of=/dev/sdc

Now, you can wait some times and take a break... The image is being 'loaded' to your lovely SD card !

At the end, you can read something like this

706+1 enregistrements lus
706+1 enregistrements écrits
2962227200 octets (3,0 GB) copiés, 284,085 s, 10,4 MB/s

Ensure the write cache is flushed and that it is safe to unmount your SD card

> sudo sync

Remove SD card from card reader and plug-it :)


SSH
---

Search the raspbian IP on private network (nmap needed)

> nmap -sV --open 192.168.0.0/25 -p22

ssh pi@[The_Raspbian_IP]

login : pi
password : raspberry


config.txt
----------

Then edit if needed your general config file (for raspbian)

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
