# Generic Model of an I/O Module
- Connected to system bus
	- Address lines
	- Data lines
	- Control lines
- Links to peripheral devices

# External Device
- Provides exchange of data between external environment and computer
- Attached via link to I/O module
	- Exchanges control, status, and data
- Peripheral device
	- External device connected to an I/O module

# Three Categories of External Devices
- Human readable
	- Communication with user
	- VDTs, printers
- Machine readable
	- Communication with equipment
	- Magnetic disks, tapes, sensors, actuators
- Communication
	- Communication with remote devices
	- Terminal, other computers

# Block Diagram of an External Device
- Control signals from I/O module
- Status signals to I/O module
- Data bits to/from I/O module
- Internal components:
	- Control logic
	- Buffer
	- Transducer
- Device-unique data exchanged with environment

# Keyboard / Monitor
- Most common computer-user interaction
- Keyboard provides input
- Monitor displays output
- International Reference Alphabet (IRA)
	- Basic unit: character
	- Each character has a unique 7-bit binary code
	- 128 characters possible

## Character Types
- Printable
	- Alphabetic, numeric, special characters
- Control
	- Control display/printing
	- Example: carriage return
	- Used in communication procedures

## Keyboard Codes
- Key press generates electronic signal
- Transducer translates signal to IRA code
- Bit pattern sent to I/O module
- On output:
	- IRA code sent to external device
	- Transducer interprets and generates required signals

# Major Functions of an I/O Module
- Control and timing
	- Coordinates internal and external flow
- Processor communication
	- Command decoding
	- Data transfer
	- Status reporting
	- Address recognition
- Device communication
	- Commands
	- Status info
	- Data exchange
- Data buffering
	- Balances speed differences
- Error detection
	- Detects and reports transmission errors

# Block Diagram of an I/O Module
- Interface to system bus
	- Data registers
	- Status/control registers
	- I/O logic
- Interface to external device
	- External device interface logic
	- Data, status, control lines

# I/O Techniques
- Programmed I/O
- Interrupt-driven I/O
- Direct Memory Access (DMA)

## Programmed I/O
- Processor exchanges data directly with I/O module
- Processor controls I/O via program
- Processor waits until operation completes
- Wasteful if processor is faster

## Interrupt-Driven I/O
- Processor issues I/O command
- Continues executing other instructions
- I/O module interrupts processor when ready
- Processor services interrupt and resumes work

## Direct Memory Access (DMA)
- I/O module transfers data directly to/from memory
- No processor involvement during transfer

# Comparison of I/O Techniques
- Programmed I/O
	- CPU moves data
	- CPU constantly checks (busy wait)
	- High CPU usage
	- Ideal for simple devices
- Interrupt-Driven I/O
	- CPU moves data
	- CPU notified on each data
	- Medium CPU usage
	- Ideal for keyboard, mouse
- DMA
	- DMA module moves data
	- CPU notified at end of block
	- Very low CPU usage
	- Ideal for disks, network, video

# I/O Commands
- Control
	- Activate peripheral
- Test
	- Check status conditions
- Read
	- Get data from peripheral into buffer
- Write
	- Send data from bus to peripheral

# I/O Instructions
- In programmed I/O:
	- Instructions correspond closely to I/O commands
- Device addressing
	- Each I/O device has unique address
	- I/O module checks address lines

## Memory-Mapped I/O
- Single address space for memory and I/O
- I/O appears as memory read/write
- No special I/O commands
- Uses same read/write lines

## Isolated I/O
- Separate address spaces
- Requires I/O or memory select lines
- Special I/O instructions
- Limited instruction set

# Interrupt-Driven I/O (Detailed)
- Processor issues command and continues work
- I/O module interrupts when ready
- Processor:
	- Finishes current instruction
	- Acknowledges interrupt
	- Saves PC and PSW to stack
	- Disables further interrupts
	- Loads ISR address
- ISR:
	- Saves registers
	- Processes interrupt
	- Restores registers
	- Executes return-from-interrupt
- Processor restores PC and PSW
- Execution resumes

## Interrupt Characteristics
- Context saved on stack (push)
- Restored on completion (pop)
- Interrupts can be nested
- Priority levels possible

## Masking Interrupts
- Multiple interrupt lines with priorities
- Higher-priority interrupts can preempt
- Lower-priority interrupts masked
- NMI (Non-Maskable Interrupt)
	- Always serviced
	- Used for critical events

# Design Issues in Interrupt I/O
- How to identify device that generated interrupt?
- How to prioritize multiple interrupts?

## Device Identification Techniques
- Multiple interrupt lines
- Software poll (non-vectored)
	- Processor polls each module
	- Time-consuming
- Daisy chain (vectored)
	- Interrupt acknowledge passed along modules
	- Vector identifies device
- Bus arbitration (vectored)
	- Module gains bus control
	- Places vector on data lines

# Drawbacks of Programmed and Interrupt I/O
- Transfer rate limited by processor speed
- CPU heavily involved in transfer
- Inefficient for large data blocks

# DMA
- DMA module transfers block directly to/from memory
- CPU only involved at start and end

## DMA Modes
- Burst mode
	- CPU waits until block transfer finishes
- Cycle stealing
	- DMA steals cycles intermittently
	- Less impact on CPU

# Evolution of I/O Function
- CPU directly controls peripheral
- I/O module added (programmed I/O)
- Interrupt-driven I/O
- DMA support
- I/O channel
	- Specialized processor for I/O
- I/O processor
	- Own memory and instruction set

# I/O Channel Architecture
- I/O module acts as specialized processor
- Reduces CPU involvement

# USB (Universal Serial Bus)
- Common peripheral interface
- Default for slow devices
- High-speed versions available
- USB 1.0
	- 1.5 Mbps (Low Speed)
	- 12 Mbps (Full Speed)
- USB 2.0
	- 480 Mbps
- USB 3.0
	- 5 Gbps signaling
	- ~4 Gbps usable
- USB 3.1 / 3.2
	- 10 Gbps (SuperSpeed+)
	- 20 Gbps (3.2)
- Hierarchical tree topology
- Controlled by root host controller

# FireWire (IEEE 1394)
- High-performance serial bus
- Daisy chain configuration
- Up to 63 devices
- Hot plugging supported
- Automatic configuration

# SCSI
- Small Computer System Interface
- Shared parallel bus
- Up to 16 or 32 devices
- Speeds from 5 Mbps to 640 MB/s
- Used in enterprise storage

# Thunderbolt
- Developed by Intel and Apple
- Combines data, video, audio, power
- Up to 10 Gbps per direction
- Up to 10W power delivery

# Infiniband
- High-end server I/O specification
- Switch-based fabric
- Connects up to 64,000 devices
- Used for storage area networks

# PCI Express
- High-speed peripheral bus
- Supports wide range of device speeds

# SATA
- Serial ATA for disk storage
- Up to 6 Gbps
- Widely used in desktops and embedded systems

# Ethernet
- Predominant wired networking
- From 3 Mbps to hundreds of Gbps
- Shift from bus-based to switch-based
- Central switch topology
- Speeds up to 800 Gbps

# Wi-Fi
- Predominant wireless networking
- IEEE 802.11 standards
- Used in enterprise and public hotspots
- Wi-Fi 7 (802.11be)
	- ~46 Gbps
	- 2.4 / 5 / 6 GHz bands

# Summary
- External devices and I/O modules
- Programmed I/O
- Interrupt-driven I/O
- DMA
- Interrupt controllers and identification
- I/O channels and processors
- Modern high-speed I/O technologies