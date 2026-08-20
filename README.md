# Assembly Learning Repository

This repository is a study workspace for learning computer architecture and Assembly language from the ground up. It contains two kinds of material:

- curated notes in `asm/`, written as a structured learning path;
- original reference books and tutorial material in `documents/`.

The notes are designed for beginners who do not yet know computer architecture or Assembly. They start with basic hardware concepts, then move into x86-64 Assembly syntax, registers, memory, flags, conditions, loops, stack usage, and build/run workflows.

## Table of Contents

- [Repository Goals](#repository-goals)
- [Directory Tree](#directory-tree)
- [Folder Responsibilities](#folder-responsibilities)
- [Recommended Study Order](#recommended-study-order)
- [Assembly Notes Index](#assembly-notes-index)
- [Computer Architecture Notes Index](#computer-architecture-notes-index)
- [Reference Documents](#reference-documents)
- [Tools You Will Need](#tools-you-will-need)
- [Build and Run Quick Start](#build-and-run-quick-start)
- [Naming Convention](#naming-convention)
- [How to Use This Repository](#how-to-use-this-repository)

## Repository Goals

The main goals are:

- understand how a computer works at the machine level;
- understand what CPU, RAM, cache, storage, buses, I/O, GPU, and OS support do;
- learn Assembly as a real programming language, not only as isolated instructions;
- connect high-level programming ideas like variables, conditions, loops, and functions to low-level CPU behavior;
- practice reading and writing small x86-64 Assembly programs;
- keep notes organized by topic so each file has one clear purpose.

## Directory Tree

```text
assembly/
|-- README.md                                      # Main repository guide, roadmap, and index.
|-- asm/                                           # Curated notes written for learning.
|   |-- README.md                                  # Short index for the note set.
|   |-- assembly_language_programing/              # Assembly language track. Folder name is kept as-is from the repo.
|   |   |-- 00_introduction.md                      # Quick Assembly introduction and first Windows/Linux run commands.
|   |   |-- 00_learning_path.md                    # Recommended order for learning Assembly.
|   |   |-- 01_introduction.md                     # What Assembly is, tools, file extensions, OS differences, mnemonic meanings.
|   |   |-- 02_syntax_program_structure.md         # Source layout, labels, sections, operands, comments.
|   |   |-- 03_data_variables_memory.md            # Data directives, variables, memory allocation, byte/word/dword/qword sizes.
|   |   |-- 04_registers.md                        # x86-64 register names, sizes, and common roles.
|   |   |-- 05_operators_instructions.md           # Core instructions for moving data, arithmetic, logic, shifts, addressing.
|   |   |-- 06_flags_and_compare.md                # Flags, cmp/test, signed and unsigned comparisons.
|   |   |-- 07_conditionals.md                     # Translating if/else/case into compare and jump instructions.
|   |   |-- 08_loops.md                            # Translating while/for/repeat loops into labels and jumps.
|   |   |-- 09_stack_functions.md                  # Stack, push/pop, call/ret, stack frames, calling conventions.
|   |   |-- 10_arrays_strings_addressing.md        # Arrays, strings, and x86 addressing modes.
|   |   |-- 11_macros_directives_build.md          # NASM directives, macros, object files, link workflow.
|   |   `-- 12_examples_line_by_line.md           # Small examples explained line by line.
|   `-- computer_architecture/                    # Hardware and system architecture track.
|       |-- 00_learning_path.md                    # Recommended order for architecture foundations.
|       |-- 01_introduction.md                     # Architecture vs organization, Von Neumann model.
|       |-- 02_how_computer_works.md               # Fetch-decode-execute cycle and instruction flow.
|       |-- 03_bits_bytes_numbers.md               # Bits, bytes, words, binary, hex, signed/unsigned, endian.
|       |-- 04_cpu.md                              # CPU parts: ALU, control unit, registers, pipeline, RISC/CISC.
|       |-- 05_registers_flags.md                  # Register/flag concepts from the hardware point of view.
|       |-- 06_memory_ram.md                       # RAM, memory layout, stack, heap, sections.
|       |-- 07_cache.md                            # Cache hierarchy, locality, cache lines, performance.
|       |-- 08_storage.md                          # HDD, SSD, files, storage path through the OS.
|       |-- 09_bus_io_interrupt_dma.md             # Buses, I/O, interrupts, programmed I/O, DMA.
|       |-- 10_gpu.md                              # GPU vs CPU, parallel workloads, VRAM, compute APIs.
|       |-- 11_operating_system_support.md         # Processes, virtual memory, loader, syscalls, privilege.
|       `-- 12_motherboard_and_components.md       # PC components: CPU, RAM, motherboard, GPU, PSU, cooling, firmware.
`-- documents/                                     # Original books, PDFs, and external tutorial resources.
    |-- assembly/                                  # Assembly language books and tutorial material.
    |   |-- Art_Of_Intel_x86_Assembly.pdf           # Intel x86 Assembly reference book.
    |   |-- Assembly_Language_for_x86_Processors_7th_Edition.pdf
    |   |                                             # x86 processors Assembly textbook.
    |   |-- Assembly_Language_Step_by_Step.pdf      # Beginner-friendly Assembly learning book.
    |   |-- Giao_trinh_Assembly.pdf                 # Vietnamese Assembly textbook.
    |   |-- Giao_trinh_ngon_ngu_lap_trinh_Assembly_11b55.pdf
    |   |                                             # Vietnamese Assembly programming textbook.
    |   |-- kien_truc_may_tinh_va_hop_ngu_pham_tuan_son_nasm_in_windows_cuuduongthancong_com.pdf
    |   |                                             # Computer architecture and Assembly with NASM on Windows.
    |   |-- ky_thuat_vi_xu_ly_va_lap_trih_assembly_cho_vi_xu_ly.pdf
    |   |                                             # Microprocessor techniques and Assembly programming.
    |   |-- nasm.pdf                                # NASM documentation/reference.
    |   |-- pcasm_book.pdf                          # PC Assembly Language book.
    |   |-- Springer_Guide_to_Assembly_Language_Programming_in_Linux.pdf
    |   |                                             # Assembly programming in Linux.
    |   |-- The_Art_of_64_Bit_Assembly_Volume_1_x86_64_Machine_Organization_and_Programming_Randall_Hyde_z_lib_org.pdf
    |   |                                             # x86-64 machine organization and programming.
    |   |-- The_Art_of_Assembly_Language_2nd_Edition_Randall_Hyde.pdf
    |   |                                             # General Assembly language book.
    |   `-- assembly-tutorial/                      # Downloaded tutorial with examples and images.
    |       |-- README.md                            # Tutorial text for AMD64/Intel 64 Assembly.
    |       |-- hello-world/                         # Hello world examples and build scripts.
    |       |   |-- build-linux.sh                     # Linux build script.
    |       |   |-- build-macos-sh                     # macOS build script.
    |       |   |-- hello                              # Built example binary.
    |       |   |-- hello-linux.asm                    # Linux hello world source.
    |       |   `-- hello-macos.asm                   # macOS hello world source.
    |       |-- images/                              # Images used by the tutorial.
    |       |   `-- cardiac2-s.jpg                    # CARDIAC teaching machine image.
    |       `-- instruction-set/                     # Instruction/addressing demonstration files.
    |           |-- addressing.asm                     # Addressing mode examples.
    |           `-- build.sh                         # Build script for instruction examples.
    `-- computer_architecture/                      # Computer architecture books.
        `-- Book_Computer_Organization_and_Architecture_10th_William_Stallings.pdf
                                                      # Main architecture textbook reference.
```

## Folder Responsibilities

`asm/` is the working note area. Read and edit these Markdown files while studying. The notes are intentionally shorter and more direct than the books.

`asm/assembly_language_programing/` is for Assembly language itself: syntax, variables, registers, instructions, flags, control flow, functions, arrays, strings, macros, and examples.

`asm/computer_architecture/` is for the hardware/system ideas behind Assembly: CPU, RAM, cache, storage, bus, I/O, GPU, operating system support, and motherboard components.

`documents/` is for source material. Treat it as the library. Use it when you want deeper explanations, textbook chapters, or original examples.

`documents/assembly/assembly-tutorial/` is a practical external tutorial with runnable examples. It is useful after reading the first Assembly notes.

## Recommended Study Order

Use this order if you are starting from zero:

1. Read [asm/computer_architecture/00_learning_path.md](asm/computer_architecture/00_learning_path.md).
2. Read [asm/computer_architecture/01_introduction.md](asm/computer_architecture/01_introduction.md).
3. Read [asm/computer_architecture/03_bits_bytes_numbers.md](asm/computer_architecture/03_bits_bytes_numbers.md).
4. Read [asm/computer_architecture/04_cpu.md](asm/computer_architecture/04_cpu.md).
5. Read [asm/computer_architecture/06_memory_ram.md](asm/computer_architecture/06_memory_ram.md).
6. Read [asm/assembly_language_programing/00_introduction.md](asm/assembly_language_programing/00_introduction.md).
7. Read [asm/assembly_language_programing/00_learning_path.md](asm/assembly_language_programing/00_learning_path.md).
8. Read [asm/assembly_language_programing/01_introduction.md](asm/assembly_language_programing/01_introduction.md).
9. Continue through the Assembly files from `02` to `12`.
10. Go back to architecture topics such as cache, I/O, GPU, and OS support when the Assembly examples start mentioning them.

Good rhythm:

- read one note;
- rewrite important ideas in your own words;
- type every Assembly example manually;
- change one line and predict what changes;
- build and run the file;
- debug the result if it differs from your prediction.

## Assembly Notes Index

| File | Purpose |
| --- | --- |
| [00_introduction.md](asm/assembly_language_programing/00_introduction.md) | Quick start, mental model, and first Windows/Linux run commands. |
| [00_learning_path.md](asm/assembly_language_programing/00_learning_path.md) | Overall Assembly study order. |
| [01_introduction.md](asm/assembly_language_programing/01_introduction.md) | Introduction, tool setup, file extensions, Windows/Linux run commands, mnemonic meanings. |
| [02_syntax_program_structure.md](asm/assembly_language_programing/02_syntax_program_structure.md) | Basic NASM source structure. |
| [03_data_variables_memory.md](asm/assembly_language_programing/03_data_variables_memory.md) | Variables, data sizes, memory allocation, array storage. |
| [04_registers.md](asm/assembly_language_programing/04_registers.md) | x86-64 registers and size aliases. |
| [05_operators_instructions.md](asm/assembly_language_programing/05_operators_instructions.md) | Common instruction groups and usage examples. |
| [06_flags_and_compare.md](asm/assembly_language_programing/06_flags_and_compare.md) | Flags, comparisons, signed and unsigned jumps. |
| [07_conditionals.md](asm/assembly_language_programing/07_conditionals.md) | How to write `if`, `else`, and `case` in Assembly. |
| [08_loops.md](asm/assembly_language_programing/08_loops.md) | How to write `while`, `for`, and repeat loops. |
| [09_stack_functions.md](asm/assembly_language_programing/09_stack_functions.md) | Stack operations, functions, stack frames, calling conventions. |
| [10_arrays_strings_addressing.md](asm/assembly_language_programing/10_arrays_strings_addressing.md) | Addressing modes, arrays, strings, indexed memory access. |
| [11_macros_directives_build.md](asm/assembly_language_programing/11_macros_directives_build.md) | NASM directives, macros, build/link workflow. |
| [12_examples_line_by_line.md](asm/assembly_language_programing/12_examples_line_by_line.md) | Worked examples explained line by line. |

## Computer Architecture Notes Index

| File | Purpose |
| --- | --- |
| [00_learning_path.md](asm/computer_architecture/00_learning_path.md) | Overall architecture study order. |
| [01_introduction.md](asm/computer_architecture/01_introduction.md) | What architecture means and why it matters for ASM. |
| [02_how_computer_works.md](asm/computer_architecture/02_how_computer_works.md) | How the CPU runs instructions. |
| [03_bits_bytes_numbers.md](asm/computer_architecture/03_bits_bytes_numbers.md) | Binary, hex, bytes, words, signed/unsigned values. |
| [04_cpu.md](asm/computer_architecture/04_cpu.md) | CPU internal parts and execution concepts. |
| [05_registers_flags.md](asm/computer_architecture/05_registers_flags.md) | Hardware view of registers and flags. |
| [06_memory_ram.md](asm/computer_architecture/06_memory_ram.md) | RAM, process memory layout, stack/heap/sections. |
| [07_cache.md](asm/computer_architecture/07_cache.md) | Cache hierarchy and locality. |
| [08_storage.md](asm/computer_architecture/08_storage.md) | Persistent storage and file access path. |
| [09_bus_io_interrupt_dma.md](asm/computer_architecture/09_bus_io_interrupt_dma.md) | Buses, I/O, interrupts, DMA. |
| [10_gpu.md](asm/computer_architecture/10_gpu.md) | GPU architecture and parallel workloads. |
| [11_operating_system_support.md](asm/computer_architecture/11_operating_system_support.md) | OS services, virtual memory, loader, privilege. |
| [12_motherboard_and_components.md](asm/computer_architecture/12_motherboard_and_components.md) | Physical PC components and their roles. |

## Reference Documents

Architecture:

- `documents/computer_architecture/Book_Computer_Organization_and_Architecture_10th_William_Stallings.pdf`

Assembly:

- `documents/assembly/nasm.pdf`
- `documents/assembly/pcasm_book.pdf`
- `documents/assembly/Assembly_Language_Step_by_Step.pdf`
- `documents/assembly/Assembly_Language_for_x86_Processors_7th_Edition.pdf`
- `documents/assembly/The_Art_of_Assembly_Language_2nd_Edition_Randall_Hyde.pdf`
- `documents/assembly/The_Art_of_64_Bit_Assembly_Volume_1_x86_64_Machine_Organization_and_Programming_Randall_Hyde_z_lib_org.pdf`
- `documents/assembly/Springer_Guide_to_Assembly_Language_Programming_in_Linux.pdf`

Vietnamese references:

- `documents/assembly/Giao_trinh_Assembly.pdf`
- `documents/assembly/Giao_trinh_ngon_ngu_lap_trinh_Assembly_11b55.pdf`
- `documents/assembly/kien_truc_may_tinh_va_hop_ngu_pham_tuan_son_nasm_in_windows_cuuduongthancong_com.pdf`
- `documents/assembly/ky_thuat_vi_xu_ly_va_lap_trih_assembly_cho_vi_xu_ly.pdf`

Practical tutorial:

- `documents/assembly/assembly-tutorial/README.md`
- `documents/assembly/assembly-tutorial/hello-world/hello-linux.asm`
- `documents/assembly/assembly-tutorial/instruction-set/addressing.asm`

## Tools You Will Need

For NASM x86-64 practice:

- NASM, the assembler;
- a linker such as `ld`, `gcc`, or `clang`;
- terminal access;
- optional debugger such as `gdb`;
- on Windows, MinGW-w64/MSYS2 or another linker toolchain.

Check tools:

```bash
nasm -v
gcc --version
```

Install on Debian/Ubuntu:

```bash
sudo apt update
sudo apt install nasm build-essential gdb
```

Install on Windows with Scoop:

```powershell
scoop install nasm
scoop install mingw
```

Install on Windows with Chocolatey:

```powershell
choco install nasm
choco install mingw
```

## Build and Run Quick Start

Linux raw syscall program:

```bash
nasm -f elf64 hello_linux.asm -o hello_linux.o
ld hello_linux.o -o hello_linux
./hello_linux
```

Windows with NASM and MinGW-w64:

```powershell
nasm -f win64 hello_windows.asm -o hello_windows.obj
gcc hello_windows.obj -o hello_windows.exe
.\hello_windows.exe
```

Important: Linux and Windows Assembly examples are not automatically interchangeable. Linux uses ELF files and syscall numbers. Windows uses PE/COFF executables and normally calls WinAPI or C runtime functions.

For complete starter examples, read [asm/assembly_language_programing/00_introduction.md](asm/assembly_language_programing/00_introduction.md).

## Naming Convention

Book/PDF filenames should use this convention:

- use letters, numbers, and `_`;
- do not use spaces;
- do not use `-`;
- do not use brackets, commas, parentheses, or other special characters;
- keep the file extension, such as `.pdf`.

Example:

```text
The Art of Assembly Language 2nd Edition (Randall Hyde).pdf
```

becomes:

```text
The_Art_of_Assembly_Language_2nd_Edition_Randall_Hyde.pdf
```

## How to Use This Repository

Start with the notes, not the large books. The notes give you a map. Use the books when a topic needs deeper reading.

When learning an Assembly concept:

1. Read the matching note.
2. Look at the example code.
3. Write a tiny `.asm` file yourself.
4. Assemble and link it.
5. Run it.
6. Change one value or instruction.
7. Predict the result before running again.

The most important habit is to always track:

- which register contains which value;
- whether a value is an address or actual data;
- how many bytes an instruction reads or writes;
- which flags were changed by the last comparison/arithmetic instruction;
- where control flow jumps next.
