Config Logitech Rumble Pad II

See if the logitech are recognize

	dmesg

[20454.020207] usb 3-1: USB disconnect, device number 2
[20466.997117] usb 3-1: new low-speed USB device number 3 using xhci_hcd
[20467.077435] usb 3-1: New USB device found, idVendor=046d, idProduct=c219
[20467.077440] usb 3-1: New USB device strings: Mfr=3, Product=1, SerialNumber=0
[20467.077443] usb 3-1: Product: Logitech Cordless RumblePad 2
[20467.077445] usb 3-1: Manufacturer: Logitech
[20467.077603] usb 3-1: ep 0x81 - rounding interval to 64 microframes, ep desc says 80 microframes
[20467.077609] usb 3-1: ep 0x1 - rounding interval to 64 microframes, ep desc says 80 microframes
[20467.151192] input: Logitech Logitech Cordless RumblePad 2 as /devices/pci0000:00/0000:00:14.0/usb3/3-1/3-1:1.0/input/input22
[20467.151591] logitech 0003:046D:C219.0008: input,hidraw3: USB HID v1.10 Gamepad [Logitech Logitech Cordless RumblePad 2] on usb-0000:00:14.0-1/input0
[20467.151597] hid_logitech: Force feedback for Logitech force feedback devices by Johann Deneux <johann.deneux@it.uu.se>

	lsusb

Bus 003 Device 003: ID 046d:c219 Logitech, Inc. Cordless RumblePad 2

	ls /dev/input

js0

	sudo apt-get install joystick
	sudo apt-get install jstest-gtk (non-nécessaire -> jstest gui version)

Launch test for the 'js0' controller and see button activation/deactivation

	jstest /dev/input/js0

or the graphical version

	jstest-gtk

Config controller with RaspBMC

http://wiki.xbmc.org/index.php?title=Keymap.xml
http://forum.xbmc.org/showthread.php?pid=606353%23pid606353

Getting the joystick name

	cat /proc/bus/input/devices

Logitech Logitech Cordless RumblePad 2

Go to the keymap directory

	cd /.xmbc/userdata

Make a new xml document
	
	sudo vim keymap.xml

Example of keymapping

	http://pastebin.com/4z2SVJVm
	https://raw.github.com/xbmc/xbmc/Frodo/system/keymaps/keyboard.xml

