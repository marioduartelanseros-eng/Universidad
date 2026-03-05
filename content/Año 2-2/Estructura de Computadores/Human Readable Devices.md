- External devices designed for interaction with users
- Allow humans to input data into a computer
- Allow computers to present output to users

Defined in:
- [[Tema 2 - Input Output]]
---

## Examples

- Keyboard
- Monitor (VDT – Video Display Terminal)
- Printer
- Touchscreen

---

## Input Example (Keyboard)

1. User presses a key
2. Keyboard generates an electrical signal
3. Signal translated into a character code (e.g., ASCII)
4. Code sent to the I/O module
5. CPU reads data via:
	- [[Tema 2 - Input Output#Programmed I/O|Programmed I/O]]
	- [[Tema 2 - Input Output#Interrupt-Driven I/O|Interrupt-Driven I/O]]

---

## Output Example (Monitor)

1. CPU sends character data to I/O module
2. I/O module sends signals to display
3. Display renders character

Character encoding depends on:
- [[Power of Binary Representation]]
- [[Byte Addressing]]

---

## Classification Context

External devices are classified as:

- [[Human Readable Devices]]
- Machine readable devices
- Communication devices

---

## Performance Consideration

Human-readable devices are typically:
- Slow compared to CPU
- Interrupt-driven rather than DMA-based

Related to:
- [[Tema 2 - Input Output#Programmed I/O|Programmed I/O]]
- [[Tema 2 - Input Output#Interrupt-Driven I/O|Interrupt-Driven I/O]]