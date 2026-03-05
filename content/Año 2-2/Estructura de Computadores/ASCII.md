# ASCII (American Standard Code for Information Interchange)

- Character encoding standard
- Represents characters using 7 bits
- Total of 128 possible characters
- Each character mapped to a unique binary number

Connects to:
- [[Human Readable Devices]]
- [[Power of Binary Representation]]
- [[Byte Addressing]]
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- [[Stored Program Computers]]

---

## Categories of Characters

### Printable Characters
- Uppercase letters (A–Z)
- Lowercase letters (a–z)
- Digits (0–9)
- Punctuation symbols

### Control Characters
- Non-printable
- Used for formatting and communication
- Examples:
	- LF (Line Feed)
	- CR (Carriage Return)
	- TAB
	- NULL

Related to:
- [[Tema 2 - Input Output|Interrupt-Driven I/O]]

---

## Example

Character:
A
```adoc
ASCII decimal:65
Binary (7-bit):1000001
Hex:0x41
```
---

## Extended ASCII

- Uses 8 bits (1 byte)
- 256 possible values
- Includes additional symbols and accented characters
- Not standardized globally

---

## Modern Replacement

ASCII is a subset of:
- Unicode
- UTF-8

UTF-8 maintains ASCII compatibility for the first 128 characters.

---

## Why It Matters

- Text stored in memory is binary
- Characters are encoded numerically
- Input/output devices rely on character encoding

ASCII demonstrates how abstract information is stored using the [[Power of Binary Representation]].