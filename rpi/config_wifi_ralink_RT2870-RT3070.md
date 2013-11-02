ADRESSE MAC


clef wpa-psk

Install Wifi
------------

Read http://ubuntuforums.org/showthread.php?t=1342593&highlight=rt2870
This wiki is an adaptated version from this previous post.

Tested with Ubuntu 13.04 and 3.8.0-21-generic kernel the 2013/05/21.

Connect your wifi key device.

Then check the Name/ID of your USB wifi key

	lsusb

>> Bus 002 Device 005: ID 148f:3070 Ralink Technology, Corp. RT2870/RT3070 Wireless Adapter

	dmesg

new high-speed USB device number 3 using xhci_hcd
[ 4031.936671] usb 3-2: New USB device found, idVendor=148f, idProduct=3070
[ 4031.936675] usb 3-2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 4031.936678] usb 3-2: Product: 802.11 n WLAN
[ 4031.936680] usb 3-2: Manufacturer: Ralink
[ 4031.936682] usb 3-2: SerialNumber: 1.0

Blacklisting Modules:

To begin, unplug any Ralink USB WiFi adapters and restart your computer (or unload the modules).

To use rt2870sta and blacklist rt2800usb, run the following commands in terminal:

	gksudo gedit /etc/modprobe.d/blacklist.conf

add these lines to the end of the file:

	# avoid conflicts for RT2870 device
	blacklist rt2x00usb
	blacklist rt2x00lib
	blacklist rt2800usb

Save the file, then insert your USB WiFi device.

1. Retrieve the driver from

	http://www.mediatek.com/_en/07_downloads/01_windows.php?sn=501

Download the last RT2870 driver 

2. Extract the compressed driver directory and files.
 
	tar xvfj 2010_0709_RT2870_Linux_STA_v2.4.0.1.tar.bz2
 
3. Enter the new directory
 
	cd 2010_0709_RT2870_Linux_STA_v2.4.0.1





(If you're trying to compile a second time, please note: Run "make clean" before running "make" to remove your previous attempt.)

5. Newer kernels >= 2.6.35 will fail to compile (make) the driver because the driver makes use of the functions usb_buffer_alloc() and usb_buffer_free() which were renamed in kernel 2.6.35 .. so if during the next (make && make install) step it fails with this error:

	make[2]: *** [/home/mark/Desktop/RT2870/os/linux/../../common/cmm_mac_usb.o] Error 1
	make[1]: *** [_module_/home/mark/Desktop/RT2870/os/linux] Error 2
	make[1]: Leaving directory `/usr/src/linux-headers-2.6.35-27-generic'
	make: *** [LINUX] Error 2

The fix is to cd to the driver source directory (eg. 2010_0709_RT28 70_Linux_STA_v 2.4.0.1), and run the following 3 commands which will clean the build directory and replace the old calls with the new ones:

make clean
find . -name \*.[ch] -exec grep usb_buffer_alloc "{}" ";" -exec sed -i 's/usb_buffer_alloc/usb_alloc_coherent/g' "{}" ";"
find . -name \*.[ch] -exec grep usb_buffer_free "{}" ";" -exec sed -i 's/usb_buffer_free/usb_free_coherent/g' "{}" ";"

6. Now you'll make some modifications, to add your device's USB Device ID. The following is an EXAMPLE. Using the lsusb command, it has been determined that an adapter has has the USB Device ID 1234:7777. MODIFY THESE INSTRUCTIONS TO USE YOUR USB DEV ID! You can put whatever you want for comments between */ s, they are meant to document the code.

	gedit ~/Desktop/*2870*/common/rtusb_dev_id.c

add the following line

	{USB_DEVICE(0x148F,0x3070)}, /* Ralink Technology, Corp. RT2870/RT3070 Wireless Adapter */

You'll now configure the source to be compiled with support for NetworkManager and wext. NetworkManager is Ubuntu's default graphical method for configuring networking. It provides the icon in the "notification area" aka "system tray".

5. You need to change some options in os/linux/config.mk to make it compatible with NetworkManager or more precisely Wpa supplicant. 
Open the existing file in your driver directory and change all wpa_supplicant related lines to yes (y instead of n).
 
	vim os/linux/config.mk

Change this

	# Support Wpa_Supplicant
	HAS_WPA_SUPPLICANT=n

	# Support Native WpaSupplicant for Network Maganger
	HAS_NATIVE_WPA_SUPPLICANT_SUPPORT=n

By this 

	# Support Wpa_Supplicant
	HAS_WPA_SUPPLICANT=y

	# Support Native WpaSupplicant for Network Maganger
	HAS_NATIVE_WPA_SUPPLICANT_SUPPORT=y

6. Compile and install. 
 
It is important here not to use "sudo" alone, but "sudo su" because with sudo for some reason the installation script fails to create the necessary files and folders. 

sudo su
make && make install

This installs the module rt2870sta.ko, but now you have 2 copies of it: one in

For me "uname -r" = 3.8.0-21-generic

	/lib/modules/3.8.0-21-generic/kernel/drivers/net/wireless

and another at

	/lib/modules/3.8.0-21-generic/kernel/drivers/staging/rt2870.

The one in the staging directory is the one that came with Ubuntu, which obviously doesn't work for you. 

7. Before you move your old driver, run the following commands to see if your newly compiled driver actually functions with your USB device.

	sudo modprobe -r rt2870sta
	sudo insmod /lib/modules/3.8.0-21-generic/kernel/drivers/net/wireless/rt2870sta.ko
	sudo /etc/init.d/networking restart
	sudo restart network-manager

If NetworkManager now works, congratulations.

Then delete the version of the rt2870sta module that came with Ubuntu (there are certainly better ways to do this [PLEASE ADVISE!], but this will allow the newly compiled one will load by default).
Code:
sudo mkdir ~/.rt2870.bak
sudo mv /lib/modules/`uname -r`/kernel/drivers/staging/rt2870 ~/.rt2870.bak
