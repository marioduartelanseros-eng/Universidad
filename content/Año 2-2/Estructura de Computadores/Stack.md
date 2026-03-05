
- A region of memory used for procedure execution
- Follows **Last-In, First-Out (LIFO)** behavior
- Grows and shrinks dynamically during program execution

Core to:
- Procedure Calling
- [[Program Counter (PC)]]
- Register File
- Memory Layout
- [[Stored Program Computers]]

---

## Stack Pointer (SP)

- Register x2 in RISC-V
- Points to the top of the stack
- Updated when data is pushed or popped

Related to:
- [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]]
- [[Tema 3 – Instruction Set Architecture (ISA)#5. Memory Operands|Memory Operands]]

---

## What Is Stored on the Stack?

When a procedure is called, the stack typically stores:

- Return address
- Saved registers
- Local variables
- Function parameters (if needed)

This block is called an **activation record** or stack frame.

---

## Basic Operations

### Push (store data on stack)

1. Decrement stack pointer
2. Store value at new address

### Pop (retrieve data)

1. Load value from stack
2. Increment stack pointer

These use:
- [[Tema 3 – Instruction Set Architecture (ISA)#5. Memory Operands|Memory Operands]]
- Load/store instructions

---

## Example (Procedure Call)

For a function call:

1. Save return address on stack
2. Save needed registers
3. Execute function
4. Restore registers
5. Return using saved address
---

## Memory Layout Context

Typical memory organization:

- Text segment (instructions)
- Static data
- Heap (grows upward)
- Stack (grows downward)

Related to:
- [[Byte Addressing]]
- [[Little Endian]]

---

## Why It Matters

- Enables nested function calls
- Supports recursion
- Preserves program state

The stack is essential for structured program execution in modern architectures.