- Memory is organized as a sequence of bytes
- Each memory address refers to **1 byte (8 bits)**
- Not to a word or doubleword

## Why It Matters

- A 32-bit word occupies 4 consecutive addresses
- A 64-bit doubleword occupies 8 consecutive addresses
- Instruction addresses increment by:
	- +4 for 32-bit instructions
	- +8 for 64-bit data (doubleword)

This connects to:
- [[Tema 3 – Instruction Set Architecture (ISA)#5. Memory Operands|Memory Operands]]
- [[Little Endian]]
- [[Big Endian]]
- [[Tema 3 – Instruction Set Architecture (ISA)]]

---

## Example (32-bit Word)

Suppose memory contains:
Address Byte  
0x00 F0  
0x01 AA  
0x02 14  
0x03 01

That represents one 32-bit value stored across **4 consecutive byte addresses**.

How it is interpreted depends on:
- [[Little Endian]]
- [[Big Endian]]

---

## Relation to Load/Store

In RISC-V:

- `lb` → loads 1 byte
- `lh` → loads 2 bytes
- `lw` → loads 4 bytes
- `ld` → loads 8 bytes

These instructions rely on [[Byte Addressing]].

---

## Key Concept

Memory is byte-addressed, but instructions and data can span multiple consecutive addresses.

This is fundamental to:
- [[Stored Program Computers]]
- [[Tema 3 – Instruction Set Architecture (ISA)#1. What is the ISA?|Instruction Set Architecture]]
- [[Tema 3 – Instruction Set Architecture (ISA)#11. Memory Layout|Memory Layout]]