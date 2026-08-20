# ASM notes

This note set is split into two tracks:

- `computer_architecture/`: computer architecture foundations for understanding CPU, RAM, cache, buses, I/O, GPU, and operating system support.
- `assembly_language_programing/`: learning Assembly like a programming language, from syntax to variables, registers, flags, conditions, loops, stack, and line-by-line examples.

Start here:

- `computer_architecture/00_learning_path.md`
- `assembly_language_programing/00_introduction.md`
- `assembly_language_programing/00_learning_path.md`

Reference documents in this repository:

- `documents/computer_architecture/Book_Computer_Organization_and_Architecture_10th_William_Stallings.pdf`
- `documents/assembly/assembly-tutorial/README.md`
- `documents/assembly/pcasm_book.pdf`
- `documents/assembly/Giao_trinh_Assembly.pdf`

Note: the existing folder name is `assembly_language_programing`, so the notes keep that name instead of renaming the directory.

## Build and Run `.asm` Files

Linux:

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

Use Linux examples on Linux and Windows examples on Windows. The object format, executable format, system calls, and calling convention are different.
