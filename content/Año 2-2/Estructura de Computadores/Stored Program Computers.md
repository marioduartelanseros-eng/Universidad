
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
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- Memory Layout