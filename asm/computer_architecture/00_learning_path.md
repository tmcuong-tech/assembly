# Computer Architecture Learning Path for Assembly

The goal of this track is to understand a computer from bits up to machine instructions. When learning Assembly, you are not only learning syntax; you are learning how the CPU fetches instructions, reads data from memory, changes registers, sets flags, and jumps to another instruction.

Recommended order:

1. `01_introduction.md`: what computer architecture means.
2. `02_how_computer_works.md`: the fetch-decode-execute cycle.
3. `03_bits_bytes_numbers.md`: bits, bytes, words, binary, hex, signed and unsigned values.
4. `04_cpu.md`: CPU, ALU, control unit, registers, pipeline.
5. `05_registers_flags.md`: registers and flags, best read together with Assembly notes.
6. `06_memory_ram.md`: RAM, addresses, stack, heap, endian order.
7. `07_cache.md`: cache and locality.
8. `08_storage.md`: SSD/HDD and why storage is much slower than RAM.
9. `09_bus_io_interrupt_dma.md`: buses, I/O, interrupts, DMA.
10. `10_gpu.md`: GPU and parallel processing.
11. `11_operating_system_support.md`: OS, processes, virtual memory, loader.
12. `12_motherboard_and_components.md`: PC components and their roles.

Connection to Assembly:

- Every Assembly instruction maps to a real CPU operation.
- Every variable is either bytes in RAM or a temporary value in a register.
- Every `if`, `while`, and `for` becomes comparisons plus jump instructions.
- Many Assembly bugs come from confusing data size, addresses, signed/unsigned interpretation, and flags.
