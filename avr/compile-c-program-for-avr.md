To compile a C program for an AVR chip you can user avr-gcc compiler
```
avr-gcc -DF_CPU=8000000UL -mmcu=atmega32a -std=gnu99 main.c -o main.elf
```
where `DF_CPU` sets a clock speed (and it also can be defined in program code) 
Avrdude is smart enough to work with the resulting ELF file but you can convert it explicitly to Intel HEX:
```
avr-objcopy -O ihex -j .text -j .data main.elf main.hex
```
The last step is to move a hex file into chip FLASH memory:
```
avrdude -c usbasp -p atmega32a2 -U flash:w:main.hex
```