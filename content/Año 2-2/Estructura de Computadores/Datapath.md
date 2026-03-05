- The hardware portion of the CPU that **moves and processes data**
- Contains the functional units required to execute instructions
- Works under control of the Control Unit

Core to:
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- [[ALU]]
- Register File
- [[Tema 3 – Instruction Set Architecture (ISA)#Five Stages|Five Stages]]
- [[Program Counter (PC)]]

---

## Main Components

Typical datapath includes:

- [[Program Counter (PC)]]
- Instruction Memory
- Register File
- [[ALU]]
- Data Memory
- Multiplexers (MUX)
- Adders
- Immediate Generator

The datapath moves data between these components.

---

## Datapath vs Control

- **Datapath** → Does the work (compute, move data)
- **Control Unit** → Decides what operation to perform

Control generates:
- ALU operation signals
- Register write enable
- Memory read/write
- Branch control

---

## In the 5-Stage Execution Model

1. IF – Fetch instruction  
2. ID – Decode & read registers  
3. EX – Execute (ALU operates)  
4. MEM – Access data memory  
5. WB – Write result back  

The datapath spans all these stages.

---

## Example: ADD Instruction

For:
add x2, x10, x4

Datapath actions:

1. PC fetches instruction
2. Register file outputs x10 and x4
3. ALU adds values
4. Result written back to x2
5. PC updated

---

## Why It Matters

- Determines how instructions are physically executed
- Directly impacts:
	- CPU Time
	- Instruction Count and CPI
	- Performance Summary

The datapath is the hardware realization of the [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]].