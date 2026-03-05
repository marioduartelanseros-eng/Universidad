- Special CPU register
- Holds the address of the next instruction to execute
- Automatically updated every instruction cycle

Core to:
- [[Stored Program Computers]]
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- [[Tema 3 – Instruction Set Architecture (ISA)#Five Stages|Five Stages]]

---

## Basic Operation

During execution:

1. PC → address sent to Instruction Memory
2. Instruction fetched
3. PC updated:
	- Normally: PC = PC + 4 (for 32-bit instructions)
	- If branch/jump: PC = target address

Related to:
- [[Byte Addressing]]

---

## In the 5-Stage Model

- IF (Instruction Fetch)
	- PC used to fetch instruction
- ID
	- Instruction decoded
- EX
	- ALU computes branch target
- MEM
	- Memory access (if needed)
- WB
	- Result written back

Related to:
- [[ALU]]
- [[Datapath]]

---
