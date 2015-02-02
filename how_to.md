# How to create an Arduino-based wireless presenter

## Global Goal

My goal is to develop a wireless presenter with different Arduino moduls I have.

### System working principle
foo

## Making your Arduino HID
As I have an Arduino Uno, and I want it to act as my keyboard/mouse would, I want it to be considered as an [USB-HID](http://en.wikipedia.org/wiki/USB_human_interface_device_class). But the actual software implemented on the chip doesn't enamble it [1](http://wiki.sgmk-ssam.ch/index.php?title=Arduino_Uno_R3_as_HID). So we need to flash the original soft. Therefor, we will follow [http://wiki.sgmk-ssam.ch](http://wiki.sgmk-ssam.ch/index.php?title=Arduino_Uno_R3_as_HID) tutorial :

### Install dfu-programmer
install it with:

    sudo apt-get install dfu-programmer

Once done, check if version is >=0.6.1

    dfu-programmer --version





# references
Here are listed all the websites I read through :

[Instructables : Turn your Arduino Uno into an USB-HID-Mididevice](http://www.instructables.com/id/Turn-your-Arduino-Uno-into-an-USB-HID-Mididevice/)

[Arduino USB HID Keyboard](http://mitchtech.net/arduino-usb-hid-keyboard/)
