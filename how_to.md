# How to create an Arduino-based wireless presenter

## Global Goal

My goal is to develop a wireless presenter with different Arduino moduls I have.

### System working principle
 The principle our system is pretty simple:
 1. You tell an Arduino (we'll call it `Bob`) what you want to do with your presentation (e.g. go to next or previous slide ; blank the screen ; etc.) - it's done through push buttons so far.
 2. `Bob` understand what you've said, and thus send a wireless message to another Arduino (we'll call it `Willy`)
 3. `Willy` get `Bob`'s message, transform it as an information that is understandable by your computer
 4. Your computer get `Willy`'s info and do what you want it to do.

>For technical reasons, `Bob` will communicate with `Willy` via **_XBees_ RF-shields** (actually, we'll use an _XBee_ chip, that you plug on a shield, that you plug on your Arduinos). Other possibilities you have have been listed [here](https://www.sparkfun.com/pages/wireless_guide) (you can also get a comparative assessment of wireless technologies on _slide 2_ of [this presentation about XBees](http://home.iitb.ac.in/~rahul./ITSP/wireless_comm.pdf)

## Making your Arduino HID
We'll begin... with **step 4**.

The easiest way your computer get `Willy`'s instructions is that `Willy` act as your keyboard/mouse would do. It means we want `Willy` belongs the [USB HID class](http://en.wikipedia.org/wiki/USB_human_interface_device_class).

I have an Arduino Uno, and I want it to be considered as an [USB-HID](http://en.wikipedia.org/wiki/USB_human_interface_device_class). But the actual software implemented on the chip doesn't enamble it [1](http://wiki.sgmk-ssam.ch/index.php?title=Arduino_Uno_R3_as_HID). So we need to flash the original soft. Therefor, we will follow [http://wiki.sgmk-ssam.ch](http://wiki.sgmk-ssam.ch/index.php?title=Arduino_Uno_R3_as_HID) tutorial :

### Install dfu-programmer
install it with:

    sudo apt-get install dfu-programmer

Once done, check if version is >=0.6.1 (otherwise, the `dfu-programmer` doesn't handle the 16u2 / 8u2 chip flashing: you need then to patch the software before installing it - STW in this case)

    dfu-programmer --version

### Restet & flash the so-called 16u2-chip connecting these two pins :

#### Reset
Connect these two pins together the two following pins together. Like anything else, do it at your own risks (-;

(_**N.B.** in case you have an 8u2 chip, you need a 10kOhm resistor, as presented in [this thread](http://arduino.cc/en/Hacking/DFUProgramming8U2)._)
![the two pins to be connected for 1s. or so](http://arduino.cc/en/uploads/Hacking/Uno-front-DFU-reset.png "the two pins to be connected for 1s. or so")

#### Download the new firmware
I downloaded the file `Arduino-usbserial-atmega16u2-Uno-Rev3.hex` from [this repo](https://roboticsclub.org/redmine/projects/quadrotor/repository/revisions/58d82c77908eee0e1c222f7b38691e6532deb77b/entry/arduino-1.0/hardware/arduino/firmwares/arduino-usbserial/Arduino-usbserial-atmega16u2-Uno-Rev3.hex) as recommanded in post #25 of [this thread](http://forum.arduino.cc/index.php?topic=106580.2).

#### Flash the chip
(These steps come from [this tutorial](http://wiki.sgmk-ssam.ch/index.php?title=Arduino_Uno_R3_as_HID))
First, move into the directory where the `*.hex` is. Then check if the programmer sees the 16U2: 

    sudo dfu-programmer atmega16u2 dump
    
You should get kind of a thousand of question marks. If it's the case, then go :

    sudo dfu-programmer atmega16u2 erase
    sudo dfu-programmer atmega16u2 flash --suppress-bootloader-mem TheFileYouveJustDownloaded.hex
    sudo dfu-programmer atmega16u2 reset

You should then be able to verse new scripts again on your Arduino

# references
Here are listed all the websites I read through :

[Instructables : Turn your Arduino Uno into an USB-HID-Mididevice](http://www.instructables.com/id/Turn-your-Arduino-Uno-into-an-USB-HID-Mididevice/)

[Arduino USB HID Keyboard](http://mitchtech.net/arduino-usb-hid-keyboard/)
