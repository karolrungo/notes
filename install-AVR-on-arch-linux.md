
Plugin your USB ASP programmer into USB port and run a command in your terminal:
```
lsusb
```

if programmer is recognized by your computer, you should find something like this:
```
Bus 002 Device 014: ID 16c0:05dc Van Ooijen Technische Informatica shared ID for use with libusb
```

then you need to install *avrdude* an utility to manage AVR programming:
`yay avrdude`

To be able to run `avrdude` without root privileges you need to create [[udev]] rule
```
/etc/udev/rules.d/99-avrprogrammer.rules

---
SUBSYSTEM=="usb", ATTR{idVendor}=="16c0", ATTR{idProduct}=="05dc", GROUP="uucp", MODE="0660"
```

`idVendor` and `idProduct` values are taken from `lsusb` command above.`plugdev` 

At the end you need to reload `udev`
```
sudo udevadm control --reload-rules
sudo udevadm trigger
```