# Power of Binary Representation

- All information in a computer is represented using **binary (0 and 1)**
- Binary works naturally with digital hardware
- Based on powers of 2

Binary enables representation of:
- Integers
- Floating-point numbers
- Characters
- Instructions
- Memory addresses

Connects to:
- [[Hexadecimal]]
- [[Tema 3 – Instruction Set Architecture (ISA)#Unsigned Integers|Unsigned Binary Integers]]
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- [[Stored Program Computers]]

---

## Why Binary?

- Hardware circuits have two stable states:
	- High / Low
	- 1 / 0
- Reliable and noise-resistant
- Efficient for logic design

---

## Powers of Two

An n-bit number can represent:

- Unsigned range:
	0 to 2ⁿ − 1

- Signed (2’s complement):
	−2ⁿ⁻¹ to +2ⁿ⁻¹ − 1

Examples:
- 8 bits → 256 values
- 32 bits → ~4 billion values
- 64 bits → extremely large range

This connects to:
- [[Byte Addressing]]

---

## Binary as Universal Encoding

Binary is used to encode:

- Instructions → [[Tema 3 – Instruction Set Architecture (ISA)#6. Instruction Encoding|Instruction Encoding]]
- Characters → [[ASCII]]
- Memory layout → [[Little Endian]] / [[Big Endian]]
- Data movement → [[Tema 3 – Instruction Set Architecture (ISA)#5. Memory Operands|Memory Operands]]

---

## Key Insight

Because everything is binary:

- Instructions are data
- Data can be interpreted differently depending on context
- This enables the [[Stored Program Computers]] model