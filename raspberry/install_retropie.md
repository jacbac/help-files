RetroPie
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

Once you have unmounted, [download the retropie .img](http://blog.petrockblock.com/retropie/retropie-downloads/), go to your download folder where the .img is, extract it, then (remember, that's the dangerous part)

```
sudo dd bs=4M if=RETROPIE_IMAGE_NAME.img of=/dev/YOUR_DISK
```

In my case for the `RetroPieImage_ver1.8.1` version,

```
sudo dd bs=4M if=RetroPieImage_ver1.8.1.img of=/dev/sdc
```

Now, you can wait some times and take a break... The image is being 'loaded' to your lovely SD card !

At the end, you can read something like this

```
825+0 enregistrements lus
825+0 enregistrements écrits
3460300800 octets (3,5 GB) copiés, 338,184 s, 10,2 MB/s
```

Ensure the write cache is flushed and that it is safe to unmount your SD card

```
sudo sync
```

Remove SD card from card reader and plug-it in your raspberry :)


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


RetroPie config
---------------

```
sudo raspi-config
```


Joystick config
---------------

```
cd .emulationstation
sudo rm es_input.cfg
```


<?xml version="1.0"?>
<inputList>
    <inputConfig type="keyboard" />
    <inputConfig type="joystick" deviceName="Logitech Logitech Cordless RumblePad 2">
        <input name="up" type="hat" id="0" value="1" />
        <input name="down" type="hat" id="0" value="4" />
        <input name="left" type="hat" id="0" value="8" />
        <input name="right" type="hat" id="0" value="2" />
        <input name="menu" type="button" id="2" value="1" />
        <input name="select" type="button" id="4" value="1" />
        <input name="pagedown" type="button" id="6" value="1" />
        <input name="pageup" type="button" id="5" value="1" />
        <input name="a" type="button" id="0" value="1" />
        <input name="b" type="button" id="1" value="1" />
    </inputConfig>
</inputList>


Add games roms to retropie
--------------------------

### Format

Atari 2600: .bin
Doom: .WAD
Game Boy Advance: .gba
Game Boy Color: .gbc
Game Gear: .gg
MAME: .zip
Megadrive/Genesis: .smd .md
NES: .nes
PC Engine/TurboGrafx 16: .pce
Sony Playstation 1: .img .7z
SNES: .smc


### Copy to retropie

Games must be copied to `home/pi/RetroPie/roms/` and subsequent folder

```
rsync -e ssh -avz /home/source user@ip_du_serveur:/dossier/destination/

example

rsync -e ssh -avz /home/dev/Bureau/Alex\ Kidd\ in\ Miracle\ World\ \[A\].sms  pi@192.168.0.10:/home/pi/RetroPie/roms/megadrive
```
