Lets assume that you have a simple Makefile to build your C program for avr chip:

```
# Nazwa pliku źródłowego (bez rozszerzenia)
TARGET = main

# Ścieżki
SRC = $(TARGET).c
BUILD_DIR = build
ELF = $(BUILD_DIR)/$(TARGET).elf
HEX = $(BUILD_DIR)/$(TARGET).hex

# Ustawienia AVR
MCU = atmega32a
F_CPU = 8000000UL
CFLAGS = -mmcu=$(MCU) -DF_CPU=$(F_CPU) -Os

# Kompilator
CC = avr-gcc
OBJCOPY = avr-objcopy

# Domyślny cel
all: $(BUILD_DIR) $(HEX)

# Reguła do tworzenia katalogu build
$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

# Kompilacja do ELF
$(ELF): $(SRC)
	$(CC) $(CFLAGS) -o $@ $<

# Konwersja ELF -> HEX
$(HEX): $(ELF)
	$(OBJCOPY) -O ihex $< $@

# Czyszczenie plików build
clean:
	rm -rf $(BUILD_DIR)

```

In the catalog that contains Makefile simply run
```
bear -- make 
```
It will run make normally, listen to all avr-gcc calls and generate `.compile_commands.json` file