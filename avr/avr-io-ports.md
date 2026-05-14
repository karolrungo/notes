---
tags: [avr, reference, c, registers, atmega32a]
status: solid
created: 2026-05-14
aliases: [DDRx, PORTx, PINx]
---

# 🧠 AVR I/O Register Reference (ATmega32A)

Each port (`PORTx`) consists of **three registers**:
- `DDRx` – Data Direction Register
- `PORTx` – Data Register
- `PINx` – Input Pins Address (Read-Only)

![[io-registers.png]]
---

## 🛠 Setting & Clearing Bits

### ✅ Set Bit to `1`:
```c
DDRC |= (1 << PC6); // Set PC6 as output

// Multiple bits at once:
DDRC |= (1 << PC6) | (1 << PC4) | (1 << PC3);
```

### ❌ Set Bit to `0`:
```c
DDRC &= ~(1 << PC6); // Set PC6 as input

// Multiple bits at once:
DDRC &= ~((1 << PC6) | (1 << PC4) | (1 << PC3));
```

---

## 📦 DDRx – Data Direction Register

| Bit Value | Mode       | Example                |
| --------- | ---------- | ---------------------- |
| `1`       | **Output** | `DDRC \|= (1 << PC6);` |
| `0`       | **Input**  | `DDRC &= ~(1 << PC6);` |

---

## ⚡ PORTx – Data Register

### When pin is **configured as output**:
| Bit Value | Effect       | Example                 |
| --------- | ------------ | ----------------------- |
| `1`       | Set pin HIGH | `PORTD \|= (1 << PD5);` |
| `0`       | Set pin LOW  | `PORTD &= ~(1 << PD5);` |

### When pin is **configured as input**:
| Bit Value | Effect               | Example                 |
| --------- | -------------------- | ----------------------- |
| `1`       | Enable **pull-up**   | `PORTD \|= (1 << PD5);` |
| `0`       | Tri-state (floating) | `PORTD &= ~(1 << PD5);` |

---

## 🔍 PINx – Input Register (Read-Only)

### Check if a pin is **LOW (0)**:
```c
if (!(PINC & (1 << PC6))) {
    // PC6 is LOW
}
```

### Check multiple pins are **ALL LOW**:
```c
if (!(PINC & ((1 << PC6) | (1 << PC4) | (1 << PC2)))) {
    // PC6, PC4, and PC2 are all LOW
}
```

### Check if a pin is **HIGH (1)**:
```c
if (PINC & (1 << PC6)) {
    // PC6 is HIGH
}
```

### Check if **any of multiple pins are HIGH**:
```c
if (PINC & ((1 << PC6) | (1 << PC4) | (1 << PC2))) {
    // At least one is HIGH
}
```

---

📌 *Tip:* Use `#define` to simplify bitmasking:
```c
#define PIN_MASK ((1 << PC6) | (1 << PC4) | (1 << PC2))

if (!(PINC & PIN_MASK)) {
    // All three pins are LOW
}
```
