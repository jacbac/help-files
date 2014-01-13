Xbian
=====

Installation
------------

For official and updated documentation, go to http://www.xbian.org/getting-started/install-xbian-using-linux/

First check the mount names of your SD card

```
df -h
```

For me it's often 'sdc1' for partition 1, 'sdc2' for partition 2, etc. but be carefull about that cause you maybe gonna wipe your entire HD ! And please read the doc and don't hesitate to do a 'man dd' before !

```
umount /dev/sdc1
umount /dev/sdc2
```

Once you have unmounted, download the xbian .img at http://www.xbian.org/download/, go to your download folder where the .img is, extract it, then (remember, that's the dangerous part)

```
sudo dd if=XBIAN_IMAGE_NAME.img of=/dev/YOUR_DISK
```

In my case for the xbian 1.0 beta 1.1 img (2013-09-29)

```
sudo dd if=XBian_1.0_Beta_1.1.img of=/dev/sdc
```

Now, you can wait some times and take a break... The image is being 'loaded' to your lovely SD card !

At the end, you can read something like this

```
1400832+0 records in
1400832+0 records out
534773760 bytes (535 MB) copied, 213,395 s, 2,5 MB/s
```

Ensure the write cache is flushed and that it is safe to unmount your SD card

```
sudo sync
```

Remove SD card from card reader and plug-it :)


SSH
---

Search the xbian IP on private network

```
nmap -sV --open 192.168.0.0/25 -p22
```

then connect

```
ssh xbian@[The_Xbian_IP]

login : xbian
password : raspberry

or 

login : root
password : xbian
```

config.txt
----------

Then edit if needed your general config file (for raspbian)

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
