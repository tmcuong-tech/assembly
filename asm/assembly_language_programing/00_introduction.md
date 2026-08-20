# Assembly Programming Introduction

This track teaches Assembly as a programming language, while keeping the hardware layer visible.

Assembly is useful because it shows what high-level code eventually becomes: instructions that move data, calculate values, compare flags, jump to labels, call functions, and ask the operating system for services.

## What You Will Learn

By the end of this track, you should be able to:

- read small x86-64 NASM programs;
- understand registers, memory, flags, labels, and jumps;
- write variables, conditions, loops, and functions in Assembly;
- assemble, link, and run `.asm` files on Linux and Windows;
- debug simple programs by tracking registers and memory.

## Recommended Setup

Use NASM for the examples in this note set.

You need:

- NASM: converts `.asm` source into an object file;
- a linker: converts the object file into an executable;
- a terminal: PowerShell/CMD on Windows or a shell on Linux.

Check the tools:

```bash
nasm -v
gcc --version
```

On Linux, `ld` is usually available through `binutils`. On Windows, the easiest path is often NASM plus MinGW-w64/MSYS2 `gcc`.

## First Mental Model

Most Assembly programs follow this flow:

```text
source.asm -> assembler -> object file -> linker -> executable
```

Common outputs:

- Linux: `hello.asm -> hello.o -> hello`
- Windows: `hello.asm -> hello.obj -> hello.exe`

The same idea applies on both systems, but the file format and operating system calls are different.

## Linux Quick Example

`hello_linux.asm`:

```asm
bits 64

section .data
    msg db "Hello from Linux", 10
    msg_len equ $ - msg

section .text
global _start

_start:
    mov rax, 1          ; write
    mov rdi, 1          ; stdout
    mov rsi, msg
    mov rdx, msg_len
    syscall

    mov rax, 60         ; exit
    xor rdi, rdi
    syscall
```

Build and run:

```bash
nasm -f elf64 hello_linux.asm -o hello_linux.o
ld hello_linux.o -o hello_linux
./hello_linux
```

## Windows Quick Example

`hello_windows.asm`:

```asm
bits 64
default rel

section .data
    msg db "Hello from Windows", 10, 0

section .text
global main
extern printf

main:
    sub rsp, 40
    lea rcx, [msg]
    call printf
    xor eax, eax
    add rsp, 40
    ret
```

Build and run with NASM and MinGW-w64:

```powershell
nasm -f win64 hello_windows.asm -o hello_windows.obj
gcc hello_windows.obj -o hello_windows.exe
.\hello_windows.exe
```

## Important Difference

A Linux syscall program usually cannot be assembled and run directly on Windows. A Windows program that calls `printf` or WinAPI also will not run directly on Linux.

Choose the example for your target operating system:

- Linux: use `elf64`, `_start`, and Linux syscalls, or link C functions with `gcc`.
- Windows: use `win64`, `main`, and C runtime or WinAPI calls.

## How To Study

Read one file at a time. Type the examples manually instead of only copying them. After each example, change one small thing and predict the result before running it again.

While reading code, always ask:

- Which register changed?
- Is this value data or an address?
- How many bytes are being read or written?
- Did the last instruction change flags?
- Where does control flow go next?
