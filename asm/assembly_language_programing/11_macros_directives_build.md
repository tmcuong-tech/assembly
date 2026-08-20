# Directives, Macros, and Build Workflow

A directive is an instruction for the assembler, not a CPU instruction.

Common NASM directives:

```asm
bits 64
section .text
section .data
section .bss
global _start
extern printf
```

Constants:

```asm
STDOUT equ 1
EXIT   equ 60
```

String length:

```asm
msg db "Hello", 10
msg_len equ $ - msg
```

`$` means the current assembler position. `msg_len` is the number of bytes from `msg` to the current position.

Repeating data:

```asm
stars times 32 db '*'
zeros times 16 db 0
```

Macro:

```asm
%macro exit 1
    mov rax, 60
    mov rdi, %1
    syscall
%endmacro

exit 0
```

Build on Linux with NASM:

```powershell
nasm -f elf64 hello.asm -o hello.o
ld hello.o -o hello
```

When calling the C library, you usually need a compiler/linker setup that includes the C runtime and libc.

Generated files:

- `.asm`: Assembly source.
- `.o`/`.obj`: object file containing machine code plus link information.
- executable: runnable file after linking.
