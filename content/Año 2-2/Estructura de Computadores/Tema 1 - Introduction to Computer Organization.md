# The Computer Revolution
- Progress in Computer Tech
	- Underpinned by [[Moore's Law]]
- Makes novel application feasible
	- Computers in automobiles
	- Cell phones
	- Human genome project
	- World Wide Web
	- Search Engines
- Computers are pervasive

# Classes of Computers
- Personal Computers
	- General purpose, variety of software
	- Subject to cost/performance tradeoff
- Server Computers
	- Network based
	- High Capacity, performance, reliability
	- Range from small servers to building sized
- Supercomputers
	- High-end scientific and engineering calculations
	- Highest capability but represent a small fraction of the overall computer market
- Embedded computers  
	- Hidden as components of systems  
	- Stringent power/performance/cost constraints

# PostPC Era
- Personal Mobile Device (PMD)
	- Battery operated
	- Connects to the internet
	- Hundreds of dollars
	- Smart phones, tablets, electronic glasses
- Cloud computing
	- Warehouse Scale Computers (WSC)
	- Software as a Service (SaaS)
	- Portion of software run on a PMD and a portion run in the Cloud
	- Amazon and Google

# Below Your Program
- Application software
	- Written in high-level language
- System Software
	- Compiler: translates High-Level language code to Machine Code
	- Operating System: Service code
		- Handling input/output
		- Managing memory and storage
		- Scheduling tasks & sharing resources
- Hardware
	- Processor, memory, [[Tema 2 - Input Output|I/O controllers]]

# Levels of Program Code
- High-Level Language
	- Level of abstraction closer to problem domain
	- Provides productivity and portability
- Assembly Language
	- Textual representation of instructions
- Hardware Representation
	- Binary digits (bits)
	- Encoded instructions and data

# Components of a Computer
- Same components for all kinds of computers
	- Desktop, server, embedded
- Input/Output includes
	- User-interface devices
		- Display, keyboard, mouse
- Storage Devices
	- Hard disk
	- CD/DVD
	- Flash
- Network adapters
	- For communicating with other computers

# Von Neumann Architecture
- Single memory for data and instructions
- Components:
	- CPU
		- Control Unit
		- Arithmetic Logic Unit (ALU)
		- Registers (PC, IR, etc.)
	- Memory Unit
	- Input Device
	- Output Device
- Instructions and data share the same memory and bus

# Harvard Architecture
- Separate program and data memories
- Independent buses for:
	- Instruction address
	- Data address
- Allows simultaneous access to instructions and data

# Touchscreen
- PostPC device
- Supersedes keyboard and mouse
- Types:
	- Resistive
	- Capacitive
		- Used in most tablets and smartphones
		- Allows multiple touches simultaneously

# Opening the Box
- Capacitive multitouch LCD screen
- 3.8V, 25 Watt-hour battery
- Computer board

# Inside the Processor (CPU)
- Datapath
	- Performs operations on data
- Control
	- Sequences datapath and memory
- Cache Memory
	- Small fast SRAM
	- Immediate access to frequently used data
- Example: Apple A5

# A Safe Place for Data
- Volatile main memory
	- Loses instructions and data when power off
- Non-volatile secondary memory
	- Magnetic disk
	- Flash memory
	- Optical disk (CDROM, DVD)

# Networks
- Purpose:
	- Communication
	- Resource sharing
	- Nonlocal access
- LAN
	- Ethernet
- WAN
	- Internet
- Wireless
	- WiFi
	- Bluetooth

# Technology Trends
- Electronics technology continues to evolve
	- Increased capacity and performance
	- Reduced cost
- Evolution:
	- Vacuum tube (1951)
	- Transistor (1965)
	- Integrated Circuit (1975)
	- VLSI (1995)
	- Ultra Large Scale IC (2013)
- DRAM capacity increases over time

# Manufacturing ICs
- Yield
	- Proportion of working dies per wafer
- Process:
	- Silicon ingot
	- Slicing into wafers
	- Processing steps
	- Testing
	- Packaging
	- Shipping

# Intel Core i7 Wafer
- 300mm wafer
- 280 chips
- 32nm technology
- Each chip: 20.7 × 10.5 mm

# Defining Performance
- Performance depends on metric
	- Passenger capacity
	- Cruising range
	- Cruising speed
	- Passengers × mph
- Must clearly define what “best performance” means

# Response Time and Throughput
- Response Time
	- Time to complete a task
- Throughput
	- Tasks per unit time
- Affected by:
	- Faster processor
	- More processors
- Focus on response time

# Relative Performance
- Performance = 1 / Execution Time
- Speedup:
	- Speedup = Execution Time_Y / Execution Time_X
	- If A takes 10s and B takes 15s
		- A is 1.5× faster than B

# Measuring Execution Time
- Elapsed Time
	- Total response time
		- Processing
		- I/O
		- OS overhead
		- Idle time
- CPU Time
	- Time CPU spends executing a job
		- User CPU time
		- System CPU time

# CPU Clocking
- Clock controls digital hardware
- Clock Period
	- Duration of one cycle
- Clock Frequency
	- Cycles per second (Hz)
	- GHz = 10⁹ Hz

# CPU Time
- CPU Time =
	- CPU Clock Cycles × Clock Cycle Time
	- CPU Clock Cycles / Clock Rate
- Improve performance by:
	- Reducing clock cycles
	- Increasing clock rate
- Tradeoff between clock rate and cycle count

# Instruction Count and CPI
- Instruction Count (IC)
	- Depends on program, ISA, compiler
- CPI (Cycles per Instruction)
	- Depends on hardware
	- Affected by instruction mix
- Clock Cycles = IC × CPI
- CPU Time = (IC × CPI) / Clock Rate

# RISC vs CISC
- RISC
	- Many simple instructions
	- High instruction count
	- Low CPI
- CISC
	- Fewer complex instructions
	- Low instruction count
	- High CPI
- Performance depends on IC × CPI

# CPI in More Detail
- Different instruction classes may have different CPI
- Weighted average CPI:
	- Based on relative frequency of instruction classes
- Clock Cycles =
	- Sum of (CPI_i × Instruction Count_i)

# Performance Summary
- Performance depends on:
	- Algorithm
	- Programming language
	- Compiler
		- Affect IC and CPI
	- ISA
		- Affects IC, CPI, clock time
- CPU Time =
	- Instructions/Program × Cycles/Instruction × Seconds/Cycle

# Power Trends
- In CMOS:
	- Power ≈ ½ × C × V² × f
- Reducing voltage greatly reduces power
- Power wall:
	- Cannot reduce voltage indefinitely
	- Heat removal is limited

# Reducing Power
- Example:
	- Reduced capacitive load
	- Reduced voltage
	- Reduced frequency
- Power reduction proportional to:
	- C × V² × f

# Uniprocessor Performance
- Limited by:
	- Power
	- Instruction-level parallelism
	- Memory latency

# Multiprocessors
- Multicore processors
	- Multiple processors per chip
- Requires parallel programming
	- Load balancing
	- Communication
	- Synchronization
- Harder than exploiting instruction-level parallelism

# SPEC CPU Benchmark
- Benchmarks represent typical workloads
- SPEC develops standardized benchmarks
- SPEC CPU2006:
	- Focus on CPU performance
	- Uses elapsed time
	- Normalized to reference machine
	- Geometric mean of performance ratios
		- CINT2006 (integer)
		- CFP2006 (floating-point)

# Pitfall: Amdahl’s Law
- Improving only part of a system limits total speedup
- Speedup =
	- 1 / (Unaffected fraction + Affected fraction / Improvement factor)
- Make the common case fast
- Some improvements cannot achieve large overall gains

# Pitfall: MIPS as a Performance Metric
- MIPS = Millions of Instructions Per Second
- Problems:
	- Different ISAs
	- Different instruction complexities
	- CPI varies across programs
- Not a reliable standalone performance metric

# Concluding Remarks
- Cost/performance keeps improving
- Systems use hierarchical abstraction
	- Hardware and software
- ISA is hardware/software interface
- Execution time is best performance measure
- Power limits performance growth
	- Parallelism used to improve performance
