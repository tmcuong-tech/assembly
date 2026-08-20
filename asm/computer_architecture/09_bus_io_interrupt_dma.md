# Buses, I/O, Interrupts, and DMA

A bus/interconnect connects CPU, RAM, and devices.

Common signal roles:

- Data: carries data.
- Address: selects the address to read/write.
- Control: read, write, interrupt, acknowledge, and other control signals.

I/O lets a computer communicate with the outside world:

- keyboard and mouse;
- display;
- network;
- USB;
- storage;
- audio.

Programmed I/O:

- The CPU manually reads/writes data to the device.
- Simple, but wastes CPU time.

Interrupt-driven I/O:

- A device notifies the CPU when an event happens.
- The CPU temporarily runs an OS interrupt handler, then returns.

DMA:

- Direct Memory Access lets a controller move data between a device and RAM without the CPU copying every byte.
- The CPU configures source/destination address, size, and permissions.

Assembly connection:

- User-mode programs normally use syscalls instead of `in`/`out` instructions.
- Kernels and drivers are the code that usually works with I/O ports, memory-mapped I/O, and interrupt handlers.
