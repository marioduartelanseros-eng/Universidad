# Hexadecimal

- Base-16 number system
- Uses digits:
	- 0–9
	- A, B, C, D, E, F (represent 10–15)
- 1 hex digit = 4 bits

This makes it a compact way to represent binary values.

---

## Why It Is Used in Computer Architecture

- Binary is long and hard to read
- Hex maps cleanly to binary
- Common for:
	- Memory addresses
	- Machine code
	- Instruction encoding
	- Debugging

Connects to:
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- [[Stored Program Computers]]
- [[Byte Addressing]]
- [[Tema 3 – Instruction Set Architecture (ISA)#5. Memory Operands|Memory Operands]]

---

## Binary ↔ Hex Mapping

| Hex | Binary |
|-----|--------|
| 0   | 0000   |
| 1   | 0001   |
| 2   | 0010   |
| 3   | 0011   |
| 4   | 0100   |
| 5   | 0101   |
| 6   | 0110   |
| 7   | 0111   |
| 8   | 1000   |
| 9   | 1001   |
| A   | 1010   |
| B   | 1011   |
| C   | 1100   |
| D   | 1101   |
| E   | 1110   |
| F   | 1111   |

---

## Example

Binary:
1110 1100 1010 1000 0110 0100 0010 0000

Grouped into 4-bit blocks → convert each block to hex:
E C A 8 6 4 2 0

Hexadecimal: 0xECA86420

---

## Relation to ISA

- RISC-V instructions are 32 bits
- Often shown in hex for readability
- Memory addresses are typically written in hex

Example:
0x00000004

Instead of:
00000000000000000000000000000100
