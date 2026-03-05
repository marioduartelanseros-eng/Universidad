- Most significant byte (MSB) stored at the lowest memory address
- Opposite of [[Little Endian]]
- Used in some network protocols and older architectures
## Example (32-bit value)
Value (hex):
0xF0AA1401
### Big Endian memory layout:

| Address | Byte |
|---------|------|
| 0x00    | F0   |
| 0x01    | AA   |
| 0x02    | 14   |
| 0x03    | 01   |
### Comparison
In [[Little Endian]] the same value would be stored as:

| Address | Byte |
|---------|------|
| 0x00    | 01   |
| 0x01    | 14   |
| 0x02    | AA   |
| 0x03    | F0   |
## Related Concepts
- [[Little Endian]]
- [[Tema 3 – Instruction Set Architecture (ISA)#5. Memory Operands|Memory Operands]]
- [[Byte Addressing]]
- [[Tema 3 – Instruction Set Architecture (ISA)]]