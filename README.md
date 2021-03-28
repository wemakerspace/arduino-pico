# Arduino-Pico [![Join the chat at https://gitter.im/arduino-pico/community](https://badges.gitter.im/arduino-pico/community.svg)](https://gitter.im/arduino-pico/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)



Raspberry Pi Pico Arduino core, for all RP2040 boards

This is a port of the RP2040 (Raspberry Pi Pico processor) to the Arduino ecosystem.

It uses a custom toolset with GCC 10.2 and Newlib 4.0.0, not depending on system-installed prerequisites.  https://github.com/earlephilhower/pico-quick-toolchain

There is automated discovery of boards in bootloader mode, so they show up in the IDE, and the upload command works using the Microsoft UF2 tool (included).

# Installing via Arduino Boards Manager
**Windows Users**: Please do not use the Windows Store version of the actual Arduino application
because it has issues detecting attached Pico boards.  Use the "Windows ZIP" or plain "Windows"
executable (EXE)  download direct from https://arduino.cc. and allow it to install any device
drivers it suggests.  Otherwise the Pico board may not be detected.  Also, if trying out the
2.0 beta Arduino please install the release 1.8 version beforehand to ensure needed device drivers
are present.  (See #20 for more details.)

Open up the Arduino IDE and go to File->Preferences.

In the dialog that pops up, enter the following URL in the "Additional Boards Manager URLs" field:

https://github.com/wemakerspace/arduino-pico/releases/download/global/package_rp2040_index.json

![image](https://user-images.githubusercontent.com/11875/111917251-3c57f400-8a3c-11eb-8120-810a8328ab3f.png)

Hit OK to close the dialog.

Go to Tools->Boards->Board Manager in the IDE

Type "pico" in the search box and select "Add":

![image](https://user-images.githubusercontent.com/11875/111917223-12063680-8a3c-11eb-8884-4f32b8f0feb1.png)


# Installing both Arduino and CMake
Tom's Hardware presented a very nice writeup on installing `arduino-pico` on both Windows and Linux, available at https://www.tomshardware.com/how-to/program-raspberry-pi-pico-with-arduino-ide

If you follow Les' step-by-step you will also have a fully functional `CMake`-based environment to build Pico apps on if you outgrow the Arduino ecosystem.

# Uploading Sketches
To upload your first sketch, you will need to hold the BOOTSEL button down while plugging in the Pico to your computer.
Then hit the upload button and the sketch should be transferred and start to run.

After the first upload, this should not be necessary as the `arduino-pico` core has auto-reset support. 
Select the appropriate serial port shown in the Arduino Tools->Port->Serial Port menu once (this setting will stick and does not need to be
touched for multiple uploads).   This selection allows the auto-reset tool to identify the proper device to reset.
Them hit the upload button and your sketch should upload and run.

In some cases the Pico will encounter a hard hang and its USB port will not respond to the auto-reset request.  Should this happen, just
follow the initial procedure of holding the BOOTSEL button down while plugging in the Pico to enter the ROM bootloader.

# Maker Pi Pico
Plug in the ESP-01 into the Maker Pi Pico

Ensure Board Selection is Raspberry Pi Pico, with debug port as `Serial` (Serial = USB CDC, Serial1 = UART0, Serial2 = UART1)

Go to File -> Example -> rp2040 and select The Maker Pi Pico demo

Raspberry Pi Pico Pinout

![image](https://user-images.githubusercontent.com/51473817/112531983-3880f480-8de3-11eb-940d-43d7d9345abb.png)

# Basic Blynk Support
Download and register account for Blynk mobile App.

Get the Blynk AUTH TOKEN from email and paste it into the example sketch.

Enter your WIFI SSID and PASSWORD into the example sketch.

Select GENERIC BOARD as your board in Blynk App, you can create a button on Pin 25 to test the build in LED.

Select the correct Port for your Maker Pi Pico.

Upload the code and open serial monitor to see the Wifi connection status.


# Status of Port
Added support for Cytron Maker Pi Pico (UART0 Change from GP00,GP01 to GP16,GP17)

Added Blynk support

Lots of things are working now!
* digitalWrite/Read (basic sanity tested)
* shiftIn/Out (tested using Nokia5110 https://github.com/ionpan/Nokia5110)
* SPI (tested using SdFat 2.0 https://github.com/greiman/SdFat ... note that the Pico voltage regulator can't reliably supply enough power for a SD Card so use external power, and adjust the `USE_SIMPLE_LITTLE_ENDIAN` define in `src/sdfat.h` to 0)
* analogWrite/PWM (tested using Fade.ino)
* tone/noTone (using IRQ generated waveform)
* Wire/I2C (tested using DS3231 https://github.com/rodan/ds3231)
* EEPROM (tested examples)
* USB Serial(ACM) w/automatic reboot-to-UF2 upload)
* Hardware UART
* Servo (basic waveform testing, disables/re-enables without any short pulses)
* printf (i.e. debug) output over USB serial 

The RP2040 PIO state machines (SMs) are used to generate jitter-free:
* Servos
* Tones

# Todo
Some major features I want to add are:
* Installable filesystem support (SD, LittleFS, etc.)
* Updated debug infrastructure
* I2S port from pico-extras

# Tutorials from Across the Web
Here are some links to coverage and additional tutorials for using `arduino-pico`
* Arduino Support for the Pi Pico available! And how fast is the Pico? - https://youtu.be/-XHh17cuH5E

# Contributing
If you want to contribute or have bugfixes, drop me a note at <earlephilhower@yahoo.com> or open an issue/PR here.

-Earle F. Philhower, III
 earlephilhower@yahoo.com
