
TODO:
What are fuse bits

In order to read the fuse bits from your microcontroller you should first [[connect-USB-ASP-programmer-with-AVR-processor]]. Then run a below command:
`avrdude -c usbasp -p m32 -B 10 -U lfuse:r:-:i -U hfuse:r:-:i`
where `-p` specifies your chip type and `-B` slows SPI clock if necessary.

Possible output:
```
Set SCK frequency to 93750 Hz

Processing -U lfuse:r:-:i
Reading lfuse memory ...
Writing 1 byte to output file <stdout>
:01000000E11E
:00000001FF

Processing -U hfuse:r:-:i
Reading hfuse memory ...
Writing 1 byte to output file <stdout>
:010000009966
:00000001FF
```

ATmega32A has 2 fuse bytes: lfuse (lower byte) and hfuse (higher byte). AVR prcessors use [[Intel-HEX-format]]
in this case
```
lfuse = 0xE1 = 1110 0001
hfuse = 0x99 = 1001 1001 
```