
# 1. What is the ISA?

- Instruction Set Architecture (ISA)
       - The repertoire of instructions of a computer
	- Interface between [[Tema 1 - Introduction to Computer Organization#Below Your Program|Hardware]] and [[Tema 1 - Introduction to Computer Organization#Below Your Program|System Software]]
	- Defines:
		- Instructions
		- Registers
		- Data types
		- Memory addressing
		- Instruction formats

- Direct continuation of:
	- [[Tema 1 - Introduction to Computer Organization#Levels of Program Code|Levels of Program Code]]
	- [[Tema 1 - Introduction to Computer Organization#Von Neumann Architecture|Von Neumann Architecture]]
	- [[Tema 1 - Introduction to Computer Organization#Measuring Execution Time|CPU Time]]
	- [[Tema 1 - Introduction to Computer Organization#RISC vs CISC|RISC vs CISC]]

---

# 2. RISC-V ISA

- Open ISA developed at UC Berkeley
- Example ISA used throughout the course
- Typical modern RISC design

## Design Principles
- Simplicity favors regularity
- Smaller is faster
- Good design demands good compromises

Connects with:
- [[Tema 1 - Introduction to Computer Organization#Performance Summary|Performance Summary]]
- [[Tema 1 - Introduction to Computer Organization#Power Trends|Power Trends]]
- [[Tema 1 - Introduction to Computer Organization#RISC vs CISC|RISC vs CISC]]

---

# 3. Instruction Basics

- Arithmetic format:
	- Two sources + one destination
	- `add rd, rs1, rs2`

- Example:
	```c
	C code
	f = (g + h) - (i + j);
	```
```C
		Compiled RISC-V
		add t0, g, h //temp t0= g+h
		add t1, i, j //temp t1= i+j
		sub f, t0, t1//f=t0-t1
```
- Requires:
	- Registers
	- ALU
	- Memory load/store

Connects with:
- [[#5. Memory Operands]]
- [[Tema 1 - Introduction to Computer Organization#Inside the Processor (CPU)|Inside the Processor (CPU)]]
- [[Tema 1 - Introduction to Computer Organization#Von Neumann Architecture|Control Unit]]

---

# 4. Registers

- 32 × 64-bit registers (x0 – x31)
- Frequently accessed data stored here
- Faster than memory

Important registers:
- x0 → zero
- x1 → return address (ra)
- x2 → stack pointer (sp)
- x3 → global pointer (gp)
- x10–x17 → arguments
- x5–x7, x28–x31 → temporaries
- x8–x9, x18–x27 → saved registers

Connects with:
- [[#10. Procedures|Procedure Calling]]
- [[Tema 2 - Input Output#Interrupt-Driven I/O|Interrupt-Driven I/O (Detailed)]]

---

# 5. Memory Operands

- Memory is byte-addressed
- RISC-V is [[Little Endian]]
- Arithmetic operates on registers only
	- Must load from memory
	- Must store back
- RISC-V doesnt require words to be aligned in memory like other ISAs

Load/Store example:
```asm6502
   ld x9, 64(x22) 
   add x9, x21, x9
   sd x9, 96(x22)
```

Connects with:
- [[Tema 1 - Introduction to Computer Organization#A Safe Place for Data|A Safe Place for Data]]
- [[Tema 2 - Input Output#Memory-Mapped I/O|Memory-Mapped I/O]]
- [[Tema 2 - Input Output#DMA|DMA]]
- [[Little Endian]]

---

# 6. Instruction Encoding

- Instructions encoded as 32-bit words
- Machine code
- Regular instruction formats

## Formats

- R-Type
- I-Type 
- S-Type
- SB-Type (branches)
- U-Type
- UJ-Type (jumps)

Connects with:
- [[Stored Program Computers]]
- [[Tema 1 - Introduction to Computer Organization#Levels of Program Code|Levels of Program Code]]
- [[Hexadecimal]]
- [[Tema 1 - Introduction to Computer Organization#CPU Clocking|CPU Clocking]]

---

# 7. Data Representation

## Unsigned Integers
- Range: 0 to 2ⁿ−1

## 2’s Complement
- Signed representation
- MSB = sign bit
- Negation:
	- Invert bits
	- Add 1

## Sign Extension
- Extend sign bit when increasing size

Connects with:
- [[Power of Binary Representation]]
- [[ALU]]

---

# 8. Logical and Shift Operations

- and, or, xor
- slli, srli, srai
- Bit masking
- Multiplication/division by powers of 2

Connects with:
- [[ALU]]
- [[Tema 1 - Introduction to Computer Organization#Instruction Count and CPI|Instruction Count and CPI]]

---

# 9. Conditional Branches

- beq, bne
- blt, bge
- bltu, bgeu

Branch addressing:
- PC-relative
- Target = PC + (imm × 2)

Connects with:
- [[Program Counter (PC)]]
- [[ALU#In the Execution Cycle|Execution Cycle]]
- [[Tema 1 - Introduction to Computer Organization#Pitfall Amdahl’s Law|Amdahl’s Law]]

---

# 10. Procedures

## Calling Convention
1. Place arguments in x10–x17
2. jal → jump and link
3. Save registers if needed
4. Execute
5. Return via jalr

## Stack Usage
- Stack pointer (x2)
- Activation record
- Save:
	- Return address
	- Temporaries
	- Saved registers

Connects with:
- Memory Layout
- [[Stack]]
- [[Tema 2 - Input Output|Interrupt Handling]]
- [[Tema 1 - Introduction to Computer Organization#Von Neumann Architecture|Control Unit]]

---

# 11. Memory Layout

- Text segment → program code
- Static data → global variables
- Heap → dynamic allocation
- Stack → procedure frames

Connects with:
- [[Tema 1 - Introduction to Computer Organization#A Safe Place for Data|A Safe Place for Data]]
- [[Tema 2 - Input Output#DMA|DMA]]
- [[Operating System]]

---

# 12. Character Data

- ASCII
- Latin-1
- Unicode
- UTF-8 / UTF-16

Connects with:
- [[Tema 2 - Input Output#External Device|External Devices]]
- [[Tema 2 - Input Output#Keyboard Codes|Keyboard Codes]]
- [[Human Readable Devices]]

---

# 13. Hardware View (Microarchitecture)

From the HW slides:

## Core Components

- ALU
- Register File
- Instruction Memory
- Data Memory
- PC
- Control Unit
- Decoder
- Immediate Generator

## Five Stages

- IF → Instruction Fetch
- ID → Instruction Decode
- EX → Execute
- MEM → Memory
- WB → Write Back

Connects with:
- [[Tema 1 - Introduction to Computer Organization#Von Neumann Architecture|Von Neumann Architecture]]
- [[Tema 1 - Introduction to Computer Organization#Harvard Architecture|Harvard Architecture]]
- [[Tema 1 - Introduction to Computer Organization#CPU Time|CPU Time]]
- [[Tema 2 - Input Output#Interrupt-Driven I/O|Interrupt-Driven I/O]]

---

# 14. RISC vs x86

## RISC-V
- Fixed 32-bit instructions
- Load/store architecture
- Simple formats
- Regular encoding

## x86
- Variable-length instructions
- Complex addressing modes
- Backward compatibility
- CISC design

Connects with:
- [[Tema 1 - Introduction to Computer Organization#RISC vs CISC|RISC vs CISC]]
- [[Tema 1 - Introduction to Computer Organization#Performance Summary|Performance Summary]]
- [[Tema 1 - Introduction to Computer Organization#Power Trends|Power Trends]]

---

# 15. Key Pitfalls & Fallacies

- Powerful instructions ≠ better performance
- Assembly ≠ automatically faster
- Backward compatibility increases complexity

Connects with:
- [[Tema 1 - Introduction to Computer Organization#Pitfall MIPS as a Performance Metric|MIPS as Performance Metric]]
- [[Tema 1 - Introduction to Computer Organization#Pitfall Amdahl’s Law|Amdahl’s Law]]

---

# Conceptual Flow So Far

1. [[Tema 1 - Introduction to Computer Organization#The Computer Revolution|The Computer Revolution]]
2. [[Tema 1 - Introduction to Computer Organization#Classes of Computers|Classes of Computers]]
3. [[Tema 1 - Introduction to Computer Organization#Below Your Program|Below Your Program]]
4. [[Tema 1 - Introduction to Computer Organization#Von Neumann Architecture|Von Neumann Architecture]]
5. [[Tema 2 - Input Output|Input/Output Techniques]]
6. [[Tema 1 - Introduction to Computer Organization#CPU Time|CPU Time]]
7. [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]] ← You are here
ISA is the bridge between:
- Software (compiler, OS)
- Hardware (datapath, control, memory)
