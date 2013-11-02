OpenElec
========

http://openelec.tv/

Installation
------------

For official and updated documentation, go to http://wiki.openelec.tv/index.php?title=Installing_OpenELEC_on_Raspberry_Pi

SSH
---

Search the openelec IP on private network (nmap needed)

> nmap -sV --open 192.168.0.0/25 -p22

ssh openelec@[The_OpenElec_IP]
```
username: root
password: openelec
```

Config.txt
----------

In flash/ folder, the config.txt is by default in 'read only' mode, so we unmoount first this folder then mount it with rewrite rights.

> mount /flash -o remount,rw

The edit the file and add some lines

> vi flash/config.txt

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

Userdata & logs
---------------

```
  special://xbmc/ is mapped to: /usr/share/xbmc
  special://xbmcbin/ is mapped to: /usr/lib/xbmc
  special://masterprofile/ is mapped to: /storage/.xbmc/userdata
  special://home/ is mapped to: /storage/.xbmc
  special://temp/ is mapped to: /storage/.xbmc/temp
  The executable running is: /usr/lib/xbmc/xbmc.bin
  Local hostname: OpenELEC
  Log File is located: /storage/.xbmc/temp/xbmc.log
```

### Logs

> tail /storage/.xbmc/temp/xbmc.log







