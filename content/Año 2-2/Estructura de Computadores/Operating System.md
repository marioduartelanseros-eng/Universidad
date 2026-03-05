# Operating System (OS)

- System software that manages hardware resources
- Provides services to application programs
- Acts as intermediary between user programs and hardware

Connects to:
- [[Tema 1 - Introduction to Computer Organization#Below Your Program|Below Your Program]]
- [[Stored Program Computers]]
- [[Tema 2 - Input Output#Interrupt-Driven I/O|Interrupt-Driven I/O]]
- Memory Layout
- [[Tema 1 - Introduction to Computer Organization#CPU Time|CPU Time]]

---

## Main Responsibilities

### 1. Process Management
- Create and terminate processes
- Schedule CPU time
- Context switching

Related to:
- [[Program Counter (PC)]]
- [[Control Unit|Register File]]
- [[Stack]]

---

### 2. Memory Management
- Allocate and deallocate memory
- Manage virtual memory
- Protect address spaces

Related to:
- [[Tema 3 – Instruction Set Architecture (ISA)#5. Memory Operands|Memory Operands]]
- [[Byte Addressing]]
- [[Little Endian]]

---

### 3. I/O Management
- Control access to devices
- Handle interrupts
- Provide device drivers

Related to:
- [[Tema 2 - Input Output#Programmed I/O|Programmed I/O]]
- [[Tema 2 - Input Output#Interrupt-Driven I/O|Interrupt-Driven I/O]]
- [[Tema 2 - Input Output#Direct Memory Access (DMA)|DMA]]
- [[Human Readable Devices]]

---

### 4. File System Management
- Organize data on storage devices
- Provide abstraction over disks

Related to:
- [[Tema 1 - Introduction to Computer Organization#A Safe Place for Data|A Safe Place for Data]]
- [[Tema 2 - Input Output#External Device|External Devices]]

---

## Privileged vs User Mode

- User mode → applications run
- Kernel mode → OS runs with full hardware access

System calls allow programs to request OS services.

---

## Why It Matters

- Enables multitasking
- Provides security and isolation
- Improves resource utilization

The Operating System coordinates the hardware components defined in the [[Tema 3 – Instruction Set Architecture (ISA)|Instruction Set Architecture]] and the architectural model introduced in [[Tema 1 - Introduction to Computer Organization]].