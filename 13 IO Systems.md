## Chapter 13 I/O Systems

- > Device drivers - present a uniform device-access interface to the I/O susbsystem, much as system calls provide a standard interface between the application and the operating system.

- PCI bus connects fast devices; expansion bus connects all the other slower devices such as the keyboard, serial and USB ports;

- A bus is a set of wires connecting the devise to a port (serial port) on the machine.

- Small Computer System Interface (SCSI) is a bus connected to the SCSI controller

- A controller a collection of electronics that can operate a port, bus, or a device; a serial-port controller controls the signal on the wires of a serial port.

- The controller has one or more registers for data and control signals - this is how processors are able to give commands and data to a controller in order to accomplish and i/o transfer.

- The system uses two techniques to control devices: 
	+ instruction directly to device registers - specify a transfer of a byte or word to the i/o port address.
	+ memory-mapped i/o - the device control registers are mapped into the address space of the processor; in other words, communication happens from the CPU to main memory where the device registers are mapped; this is faster and more efficient than simple instructions sent directly to the i/o port address.

- I/O port consists of four main registers:
	+ data-in register - to get input 
	+ data-out register - to send output
	+ status register - bits read by the host (usually contain information about the state of the device; or device error)
	+ control register - allows for changing the mode of a device; or even enables parity checking


- > It is more efficient for the hardware controller to notify the CPU when the device becomes read for service, rather than to require the CPU to poll repeatedly for an I/O completion. The hardware mechanism that enables a device to notify the CPU is called an interrupt; this interrupt is done via the interrupt-request line which is sensed by the CPU; the task is then dispatched to the interrupt handler by the CPU, and the handler clears the interrupt by servicing the device; then the CPU resumes processing of interrupted task;

- Interrupt control hardware - handles defers of interrupt handling; dispatching to the proper interrupt handler without first polling all the devices to see which one raised the interrupt; and distinguishing between high and low level priority interrupts and can respond with the appropriate level of urgency.

- interrupt vector hold addresses that point to the head of the interrupt handlers for making it more efficient to find the appropriate interrupt handler.

- the CPU has two interrupt request lines: 
	+ non-maskable - handles memory errors
	+ maskable - handle device-generated interrupts

- Direct Memory Access (DMA) - is in charge of large transfer which are delegated from the CPU; usually hold pointer of source, destination and then operate the memory bus directly, to perform the transfers without the CPU. 

- The purpose of the device driver layer is to hide the differences among device controllers from the I/O subsystem of the kernel; this provides the creator of new devices to write device drivers for the OS to support their devices or design devices that are compatible with an existing host controller interface (such as SATA)

- Several services - scheduling, buffering, caching, spooling, device reservation, and error handling -- are provided by the kernel I/O subsystem and build on the hardware and device-driver infrastructure.

- buffer are areas of memory set aside for dealing with data transfer decoupling and data transfer size between devices or between a device and an application. also used for copy semantics (making sure that the data provided by the application is always the latest version); another way to achieve this is to copy the application buffer to the kernel buffer so that the disk write is performed from the kernel buffer.

- a cache is a region of fast memory that hold copies of data; the difference of the buffer and the cache is that the buffer usually holds the only copy of the data and the cache hold a copy the data on faster storage

-  a spool is a buffer that holds output for a device, such as a printer, that cannot accept interleaved data streams.


- Protected memory can avoid complete system malfunction. Network problems can be dealt with resubmitting system calls by the operating system. Permanent reasons (such as when device controllers become defective) are not recoverable by the OS.

- Error handling - a bit of information (errno), in form of an integer, is returned by the system call

- I/O protection - Instead of having users perform direct I/O, the request must go through the OS by means of a system call; memory protection also protect any memory-mapped and I/O port memory locations from user access. in case of memory-mapped graphics controller, for example, the kernel provides locking mechanism to protect overload on the device.

- In summary, the I/O subsystem coordinates a collection of services that are available to applications and to other parts of the kernel. The I/O subsystem supervises these procedures:
	+ management of the name space for files and devices
	+ access control to files and devices
	+ operation control
	+ file-system space allocation
	+ device allocation
	+ buffering, caching, and spooling
	+ I/O scheduling
	+ device-status monitoring, error handling, and failure recovery
	+ device-driver configuration and initialization

- The upper levels of the I/O subsystem access devices via the uniform interface provided by the device drivers.

- The device name also has the form of a name in the file-system name space. When UNIX looks up this name in the file-system directory structures, it finds not a <major,minor> device number. The major device number identifies a device driver that should be called to handle the I/O to this device. The minor device number is passed to the device driver to index into a device table. The corresponding device-table entry gives the port address or the memory-mapped address of the device controller.

