How to set bit to `0`
`DDRC &= ~(1<<PC6)`
`DDRC &= ~( (1<<PC6) | (1<<PC4) | (1<<PC3) ) //multiple bits at once`

How to set bit to `1`
`DDRC |= (1<<PC6)`
`DDRC |= (1<<PC6) | (1<<PC4) | (1<<PC3) //multiple bits at once`

Each port consists of three register: DDRn, PORTn, and PINn.

![[io-registers.png]]

**DDRn** is a data direction register:
	`1 `- **output** `DDRC |= (1<<PC6)` writes `1` to the bit PC6
	`0` - **input**  `DDRC &= ~(1<<PC6)` writes `0` to the bit PC6

**PORTn**
	When pin is configured as an **output** (through DDRn register):
	 `1`  in bit register **PORTn** sets it **high**  `PORTD |= (1<<PD5) //1`
	 `0`  in bit register **PORTn** sets it **low** `PORTD &= ~(1<<PD5) //0`
	When pin is configured as an **input**:
	 `1`  in bit register **PORTn** activates build-in**pull-up** resistor

**PINn** is an input register. It is *read-only*
	check for `0`
		`!(PINC & (1<<PC6))`
		for multiple bits `!(PINC & ((1 << PC6) | (1 << PC4) | (1 << PC2)))`
	check for `1`
		`PINC & (1 << PC6)`
		or multiple bits `PINC & ((1 << PC6) | (1 << PC4) | (1 << PC2))`