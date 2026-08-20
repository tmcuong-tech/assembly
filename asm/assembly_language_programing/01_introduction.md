# What Assembly Is

Assembly is a language close to the CPU's machine instructions. Each Assembly instruction usually maps to one CPU instruction, while directives give instructions to the assembler.

How it differs from high-level languages:

- C/Python have variables, types, `if`, `while`, and functions as high-level concepts.
- Assembly works directly with registers, memory addresses, the stack, flags, and jumps.

Assembler:

- Reads `.asm` source files.
- Translates mnemonics such as `mov`, `add`, `jmp` into machine code.
- Resolves labels, sections, directives, and macros.

Linker:

- Combines object files such as `.o` or `.obj`.
- Fixes addresses for labels/functions.
- Produces an executable file.

## Common File Extensions

Assembly work usually produces several file types:

| Extension | Meaning | Used on |
| --- | --- | --- |
| `.asm` | Assembly source code | Windows, Linux |
| `.s` | Assembly source, often used by GNU tools | Linux, Unix-like systems |
| `.inc` | Include file for constants/macros | Windows, Linux |
| `.o` | Object file | Linux, Unix-like systems |
| `.obj` | Object file | Windows |
| `.exe` | Executable program | Windows |
| no extension | Executable program | Linux |
| `.lst` | Listing file: source plus generated machine code | Optional debugging output |
| `.map` | Linker map: symbols and addresses | Optional debugging output |

Typical build pipeline:

```text
source.asm -> assembler -> object file -> linker -> executable
```

Example:

```text
hello.asm -> nasm -> hello.o -> ld/gcc -> hello
hello.asm -> nasm -> hello.obj -> gcc/link.exe -> hello.exe
```

## Required Tools

For NASM x86-64 Assembly, you usually need:

- NASM: the assembler.
- A linker: `ld`, `gcc`, `clang`, MinGW `gcc`, or Microsoft `link.exe`.
- A terminal: PowerShell/CMD on Windows, shell on Linux.
- Optional debugger: `gdb` on Linux, WinDbg/x64dbg/Visual Studio debugger on Windows.

Check whether NASM is installed:

```powershell
nasm -v
```

Check whether GCC is installed:

```powershell
gcc --version
```

## Installing Tools on Windows

Option 1: install with Scoop:

```powershell
scoop install nasm
scoop install mingw
```

Option 2: install with Chocolatey:

```powershell
choco install nasm
choco install mingw
```

Option 3: install manually:

- Download NASM from `https://www.nasm.us/`.
- Install MinGW-w64 or MSYS2 for `gcc`.
- Add the tool folders to the `PATH` environment variable.

If using MSYS2:

```powershell
pacman -S mingw-w64-x86_64-nasm
pacman -S mingw-w64-x86_64-gcc
```

## Installing Tools on Linux

Debian/Ubuntu:

```bash
sudo apt update
sudo apt install nasm build-essential gdb
```

Fedora:

```bash
sudo dnf install nasm gcc binutils gdb
```

Arch Linux:

```bash
sudo pacman -S nasm gcc binutils gdb
```

## Build and Run on Linux

Minimal Linux program using syscalls:

```asm
bits 64

section .text
global _start

_start:
    mov rax, 60     ; exit
    mov rdi, 0      ; status code
    syscall
```

Assemble, link, and run:

```bash
nasm -f elf64 hello.asm -o hello.o
ld hello.o -o hello
./hello
echo $?
```

Command meaning:

- `nasm -f elf64`: generate a 64-bit Linux object file.
- `hello.o`: object file.
- `ld hello.o -o hello`: link object file into executable named `hello`.
- `./hello`: run the program.
- `echo $?`: print the previous program's exit code.

## Build and Run on Windows

Windows executables use a different object format and a different system API. A Linux syscall program will not run directly on Windows.

With NASM and MinGW-w64:

```powershell
nasm -f win64 hello.asm -o hello.obj
gcc hello.obj -o hello.exe
.\hello.exe
```

Command meaning:

- `nasm -f win64`: generate a 64-bit Windows object file.
- `hello.obj`: Windows object file.
- `gcc hello.obj -o hello.exe`: link it into a Windows executable.
- `.\hello.exe`: run the program from PowerShell.

For a program that calls C library functions such as `printf`, link with `gcc` instead of calling `ld` directly, because `gcc` adds the required C runtime setup.

## Important Platform Differences

Linux and Windows differ in several important ways:

- Object format: Linux uses ELF (`elf64`), Windows uses PE/COFF (`win64`).
- Executable name: Linux often has no extension, Windows uses `.exe`.
- OS calls: Linux uses `syscall` numbers; Windows usually calls WinAPI functions.
- Calling convention: Linux x86-64 System V and Windows x64 pass arguments in different registers.
- Entry point: Linux raw programs often use `_start`; Windows programs usually use C runtime entry points or Windows-specific entry points.

Because of this, always choose examples for your target OS. A correct Linux Assembly file may fail on Windows, and a correct Windows Assembly file may fail on Linux.

Why learn ASM:

- Understand how computers actually run programs.
- Read debugger output and disassembly more confidently.
- Understand stack, memory, calling conventions, and overflow.
- Write low-level code when needed: OS, embedded, drivers, reverse engineering, performance work.

Vocabulary:

- instruction: a CPU operation.
- mnemonic: human-readable instruction name, such as `mov`.
- opcode: the actual machine-code number for an instruction.
- operand: the input/output value of an instruction.
- register: storage inside the CPU.
- memory address: a location in RAM.
- label: a name for an address.
- flag: a status bit after arithmetic, logic, or comparison.

## Meaning of Common Assembly Names

Assembly instruction names are often abbreviations. Knowing the full meaning makes them easier to remember.

### Data Movement

| Name | Full meaning | What it does |
| --- | --- | --- |
| `mov` | move | Copies data from source to destination. The source is not erased. |
| `xchg` | exchange | Swaps two values. |
| `lea` | load effective address | Computes an address and stores that address in a register. It does not read memory. |
| `push` | push onto stack | Stores a value on top of the stack. |
| `pop` | pop from stack | Removes the top stack value into a register or memory. |

Important: `mov` means copy, not move in the everyday sense.

```asm
mov rax, rbx
```

After this instruction:

- `rax` receives the value from `rbx`.
- `rbx` still keeps the same value.

### Arithmetic

| Name | Full meaning | What it does |
| --- | --- | --- |
| `add` | add | Adds source to destination. |
| `sub` | subtract | Subtracts source from destination. |
| `inc` | increment | Adds 1. |
| `dec` | decrement | Subtracts 1. |
| `neg` | negate | Changes the sign using two's complement. |
| `mul` | multiply | Unsigned multiplication. |
| `imul` | integer multiply | Signed multiplication. |
| `div` | divide | Unsigned division. |
| `idiv` | integer divide | Signed division. |

Example:

```asm
mov rax, 10
add rax, 5      ; rax = 15
sub rax, 3      ; rax = 12
inc rax         ; rax = 13
dec rax         ; rax = 12
neg rax         ; rax = -12
```

### Logic and Bit Operations

| Name | Full meaning | What it does |
| --- | --- | --- |
| `and` | logical AND | Keeps bits that are 1 in both operands. |
| `or` | logical OR | Sets bits that are 1 in either operand. |
| `xor` | exclusive OR | Sets bits that are different; also used to clear a register with itself. |
| `not` | logical NOT | Inverts all bits. |
| `test` | test bits | Performs AND only to set flags; does not store the result. |
| `shl` | shift left | Moves bits left, fills low bits with 0. |
| `shr` | shift right | Logical right shift, fills high bits with 0. |
| `sar` | shift arithmetic right | Right shift that preserves the sign bit. |
| `rol` | rotate left | Rotates bits left. |
| `ror` | rotate right | Rotates bits right. |

Example:

```asm
xor rax, rax    ; fast common way to set rax = 0
and al, 0Fh     ; keep only the low 4 bits of AL
or  al, 80h     ; set bit 7 of AL
```

### Comparison and Jumps

| Name | Full meaning | What it does |
| --- | --- | --- |
| `cmp` | compare | Subtracts internally to set flags; result is not stored. |
| `jmp` | jump | Unconditional jump to a label/address. |
| `je` | jump if equal | Jumps if `ZF=1`. Same as `jz`. |
| `jne` | jump if not equal | Jumps if `ZF=0`. Same as `jnz`. |
| `jz` | jump if zero | Jumps if `ZF=1`. |
| `jnz` | jump if not zero | Jumps if `ZF=0`. |
| `jg` | jump if greater | Signed `>` comparison. |
| `jge` | jump if greater or equal | Signed `>=` comparison. |
| `jl` | jump if less | Signed `<` comparison. |
| `jle` | jump if less or equal | Signed `<=` comparison. |
| `ja` | jump if above | Unsigned `>` comparison. |
| `jae` | jump if above or equal | Unsigned `>=` comparison. |
| `jb` | jump if below | Unsigned `<` comparison. |
| `jbe` | jump if below or equal | Unsigned `<=` comparison. |
| `call` | call procedure/function | Pushes return address, then jumps to a function. |
| `ret` | return | Pops return address and jumps back. |

Example:

```asm
cmp rax, 10
je equal        ; jump if rax == 10
jg greater      ; jump if rax > 10, signed
```

### System and CPU Control

| Name | Full meaning | What it does |
| --- | --- | --- |
| `syscall` | system call | Enters the operating system kernel on x86-64 Linux. |
| `int` | interrupt | Triggers a software interrupt, common in older DOS/BIOS examples. |
| `nop` | no operation | Does nothing for one instruction. Useful for alignment or patching. |
| `hlt` | halt | Stops the CPU until the next interrupt; usually kernel-level code. |

## Meaning of Data Type Directives

NASM data directives also use short names.

### Initialized Data

| Directive | Full meaning | Size allocated | Example |
| --- | --- | ---: | --- |
| `db` | define byte | 1 byte = 8 bits | `age db 25` |
| `dw` | define word | 2 bytes = 16 bits | `score dw 1000` |
| `dd` | define doubleword | 4 bytes = 32 bits | `count dd 123456` |
| `dq` | define quadword | 8 bytes = 64 bits | `total dq 0` |
| `dt` | define ten bytes | 10 bytes = 80 bits | used for old x87 floating-point data |

Example:

```asm
section .data
a db 1       ; one byte
b dw 2       ; one word, 2 bytes
c dd 3       ; one doubleword, 4 bytes
d dq 4       ; one quadword, 8 bytes
```

### Reserved / Uninitialized Data

| Directive | Full meaning | Size reserved |
| --- | --- | ---: |
| `resb` | reserve byte | 1 byte each |
| `resw` | reserve word | 2 bytes each |
| `resd` | reserve doubleword | 4 bytes each |
| `resq` | reserve quadword | 8 bytes each |
| `rest` | reserve ten bytes | 10 bytes each |

Example:

```asm
section .bss
buffer resb 64      ; 64 bytes
nums   resd 10      ; 10 * 4 = 40 bytes
big    resq 1       ; 1 * 8 = 8 bytes
```

### Size Names in x86

| Name | Meaning | Size |
| --- | --- | ---: |
| byte | 8-bit value | 1 byte |
| word | 16-bit value | 2 bytes |
| dword | doubleword, 32-bit value | 4 bytes |
| qword | quadword, 64-bit value | 8 bytes |
| tword | ten-byte value, often 80-bit floating point | 10 bytes |
| xmmword | 128-bit SIMD value | 16 bytes |
| ymmword | 256-bit SIMD value | 32 bytes |
| zmmword | 512-bit SIMD value | 64 bytes |

These names are often used to tell the assembler exactly how much memory to read or write:

```asm
mov byte  [age], 25     ; write 1 byte
mov word  [score], 100  ; write 2 bytes
mov dword [count], 10   ; write 4 bytes
mov qword [total], 500  ; write 8 bytes
```

## Register Name Patterns

Register names also contain size hints.

Using `rax` as the example:

| Name | Size | Meaning |
| --- | ---: | --- |
| `rax` | 64 bits | full 64-bit register |
| `eax` | 32 bits | low 32 bits of `rax` |
| `ax` | 16 bits | low 16 bits of `rax` |
| `al` | 8 bits | low 8 bits of `ax` |
| `ah` | 8 bits | high 8 bits of `ax` |

Example:

```asm
mov rax, 0x1122334455667788
mov al, 0xff
; rax is now 0x11223344556677ff
```
