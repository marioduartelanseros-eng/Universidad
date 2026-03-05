# ALU (Arithmetic Logic Unit)

- Core component of the CPU
- Performs arithmetic and logical operations
- Operates on register operands
- Produces a result written back to a register

Connects to:
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- [[Datapath]]
- [[Control Unit]]
- [[Tema 3 – Instruction Set Architecture (ISA)#Five Stages|Five Stages]]

---

## Main Operations

### Arithmetic
- add
- sub
- mul
- increment/decrement

Related to:
- [[Tema 3 – Instruction Set Architecture (ISA)#Unsigned Integers|Unsigned Binary Integers]]
### Logical
- and
- or
- xor
- not
### Shift
- shift left (slli)
- shift right logical (srli)
- shift right arithmetic (srai)

Related to:
- [[Power of Binary Representation]]

---

## Inputs and Outputs

Typical ALU structure:

- Input A → from register file
- Input B → from register file or immediate
- Control signal → selects operation
- Output → result to register file

So it interacts directly with:
- [[Control Unit|Register File]]
- [[Tema 3 – Instruction Set Architecture (ISA)#6. Instruction Encoding|Instruction Encoding]]

---

## In the Execution Cycle

In a classic 5-stage pipeline:

1. IF – Instruction Fetch  
2. ID – Instruction Decode  
3. EX – Execute → **ALU works here**
4. MEM – Memory access  
5. WB – Write back  

Related to:
- [[Tema 3 – Instruction Set Architecture (ISA)#Five Stages|Five Stages]]
- [[Stored Program Computers]]

---

## Why It Matters

- Determines computational capability
- Directly affects:
	- [[Tema 1 - Introduction to Computer Organization#CPU Time|CPU Time]]
	- [[Tema 1 - Introduction to Computer Organization#Instruction Count and CPI|Instruction Count and CPI]]
	- [[Tema 1 - Introduction to Computer Organization#Performance Summary|Performance Summary]]

The ALU is the hardware unit that executes the operations defined by the [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]].