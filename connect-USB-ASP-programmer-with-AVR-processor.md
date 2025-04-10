USB ASP programmer usually has a 10-pin Kanda connector and uses SPI standard to write your program into chip memory:

![350][kanda.png]]

You should connect each signal from the programmer to the corresponding pin of your microcontroller. The signals are NOT crossed so it means that you connect MOSI to MOSI, MISO to MISO etc.. 

If your physical connections are OK (please double check) you can run a command to verify if your computer can connect with a microcontroller:
```
avrdude -c usbasp -p m32
```

where a `-p` option speficies a microcontroller type (`m32` is ATmega32).

In my case I had to reduce the clock speed of the SPI bus:
```
avrdude -c usbasp -p m32 -v -B 125kHz
Avrdude version 8.0
Copyright see https://github.com/avrdudes/avrdude/blob/main/AUTHORS

System wide configuration file is /etc/avrdude.conf
User configuration file /home/rungo/.avrduderc does not exist

Using port            : usb
Using programmer      : usbasp
Setting bit clk period: 8.0 us
AVR part              : ATmega32
Programming modes     : SPM, ISP, HVPP, JTAG, JTAGmkI
Programmer type       : usbasp
Description           : USBasp ISP and TPI programmer
Set SCK frequency to 93750 Hz

AVR device initialized and ready to accept instructions
Device signature = 1E 95 02 (ATmega32, ATmega32A)
```

without `-B` option I got famous (rc = -1) error:
```
avrdude -c usbasp -p m32             
Error: program enable: target does not answer (0x01)
Error: initialization failed  (rc = -1)
 - double check the connections and try again
 - use -B to set lower the bit clock frequency, e.g. -B 125kHz
 - use -F to override this check
```
