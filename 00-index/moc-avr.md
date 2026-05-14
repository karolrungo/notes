---
title: AVR Programming - Map of Content
tags: [moc, avr, embedded, hardware]
created: 2026-05-14
status: solid
---

# AVR Programming — Map of Content

The hub for everything about programming AVR microcontrollers (mainly ATmega32A) on Arch Linux.

## Setup

Get your machine and hardware ready to flash a chip.

- [[install-avr-toolchain-on-arch-linux]] — install `avr-gcc`, `avrdude` and friends
- [[connect-usbasp-programmer-to-avr]] — wire the USBasp to the chip and verify the link

## Programming workflow

The day-to-day cycle: write code → build → flash.

- [[compile-c-program-for-avr]] — compile a C source file for the AVR target
- [[generate-compile-commands-json-with-bear]] — get IDE/LSP autocomplete working with `bear`

## Hardware concepts

What's actually happening on the chip.

- [[avr-io-ports]] — `DDRx` / `PORTx` / `PINx` register cheatsheet
- [[read-fuse-bits-atmega32a]] — read the lfuse / hfuse bytes from a chip
- [[intel-hex-format]] — the file format `avrdude` flashes onto the chip

## Related

- [[moc-linux]] — `udev` rules are required to use the USBasp programmer without root

## Open questions / next to learn

- [ ] What are fuse bits actually controlling? (clock source, brown-out, lock bits)
- [ ] How to use AVR timers and interrupts
- [ ] AVR UART / USART for serial communication
- [ ] How to read the datasheet efficiently
