`udev` is a device manager program in Linux that works dynamically.
What it does
1. **Detects** the new hardware via kernel events
2. **Creates the device file** under `/dev/` (e.g., `/dev/ttyUSB0`, `/dev/sda1`, etc.)
3. **Applies rules** to:
    - Name the device (`/dev/usbasp`, etc.)
    - Set its permissions (`MODE=0660`)
    - Assign it to a group (`GROUP="uucp"`)
    - Add access tags (`TAG+="uaccess"`)
    - Run custom actions (`RUN+=...`)

`udev rule` is a line of text / a file that tells `udev` what to do with a specific device when it is plugged into your computer, for example:
```
SUBSYSTEM=="usb", ATTR{idVendor}=="16c0", ATTR{idProduct}=="05dc", GROUP="uucp", MODE="0660"
```

Rules locations:
```
/usr/lib/udev/rules.d/ #system-wide
/etc/udev/rules.d/ #user-defined
```

Rules are processed in numerical order, so `10-...` runs before `99-...`.

Common use cases for `udev`:
- Grant access to USB programmers (like USBasp, STLink)
- Auto-mount USB drives
- Rename network interfaces
- Change permissions for serial devices (`/dev/ttyUSB0`)
- Trigger scripts when a device is plugged