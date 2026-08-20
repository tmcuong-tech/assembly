# Introduction to Computer Architecture

Computer architecture is the part of a computer that is visible to low-level programmers: instruction set, registers, data types, addressing modes, flags, calling conventions, and memory behavior. Computer organization is how hardware implements those ideas: ALU, control unit, cache, buses, pipelines, and memory controllers.

Examples:

- `mov rax, 5` is architectural: x86-64 has a register named `rax` and an instruction named `mov`.
- The number and size of L1/L2/L3 caches is organizational: two CPUs can both run x86-64 code but have different cache designs.

A modern computer is often explained with the Von Neumann model:

- CPU executes instructions.
- Memory stores both program code and data.
- I/O connects keyboard, display, storage, network, and other devices.
- Buses/interconnects move data between components.

Three questions to ask while learning ASM:

- Where is the data: register, RAM, stack, file, or I/O device?
- How large is it: 1 byte, 2 bytes, 4 bytes, or 8 bytes?
- How does the CPU know where to go next: next instruction, jump, call, return, or interrupt?
