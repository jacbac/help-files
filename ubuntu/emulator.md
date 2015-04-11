Let's have some fun, Grand'Pa !
===============================

Gamecube / Wii
--------------

With Dolphin:

```
sudo add-apt-repository ppa:glennric/dolphin-emu
sudo apt-get update
sudo apt-get install dolphin-emu-master

which dolphin-emu
/usr/games/dolphin-emu
```

Super Nintendo
--------------

With Snes9x:

```
sudo apt-get install zsnes

which zsnes
/usr/bin/zsnes
```

Nintendo 64
-----------

With Mupen64 & M64Py (Mupen64 GUI):

```
sudo add-apt-repository ppa:sven-eckelmann/ppa-mupen64plus
sudo apt-get update
sudo apt-get install mupen64plus

which pcsxr
/usr/games/pcsxr
```

Playstation 1
-------------

```
sudo add-apt-repository ppa:rebuntu16/pcsx-reloaded-svn+unofficial
sudo apt-get update
sudo apt-get install pcsxr

which pcsxr
/usr/games/pcsxr
```

PlayStation 2
-------------

With PCSX2:

```
sudo add-apt-repository ppa:gregory-hainaut/pcsx2.official.ppa
sudo apt-get update
sudo apt-get install pcsx2
```

MAME
----

```
sudo add-apt-repository ppa:c.falco/mame
sudo apt-get update
sudo apt-get install mame

which mame
/usr/games/mame
```

Sega Genesis / Master System
----------------------------

With Kega-Fusion:

* Download .deb package from the [official kega-fusion page](http://www.carpeludum.com/kega-fusion/)
* If you’re using a 64-bit version of Ubuntu, remember to install the 32-bit architecture packages before installing the following .deb package first:

```
sudo dpkg --add-architecture i386
sudo apt-get update
sudo dpkg -i kega-fusion_3.xx_i386.deb
```

and I get this message:

```
kega-fusion dépend de libglu1-mesa.
kega-fusion dépend de libsm6.
kega-fusion dépend de libgtk2.0-0.
kega-fusion dépend de libasound2-plugins.
kega-fusion dépend de libmpg123-0.
kega-fusion dépend de gtk2-engines-murrine.
kega-fusion dépend de gtk2-engines-pixbuf.
```

so:

```
sudo apt-get install libglu1-mesa:i386 libgtk2.0-0:i386 libasound2:i386 libsm6:i386 libasound2-plugins:i386 gtk2-engines-oxygen:i386
sudo apt-get -f install
sudo dpkg -i kega-fusion_3.xx_i386.deb

which kega-fusion
/usr/games/kega-fusion
```
