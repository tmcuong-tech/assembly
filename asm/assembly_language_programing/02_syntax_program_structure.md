# Syntax and Program Structure

An Assembly line often has this shape:

```asm
label:  instruction  operand1, operand2  ; comment
```

Parts:

- `label`: a name for the current address.
- `instruction`: a CPU instruction or assembler directive.
- `operand`: register, memory, immediate value, or label.
- `comment`: text after `;`, ignored by the assembler.

NASM Linux x86-64 example:

```asm
bits 64

section .text
global _start

_start:
    mov rax, 60     ; syscall exit
    mov rdi, 0      ; exit code 0
    syscall
```

Common sections:

- `.text`: machine code.
- `.data`: initialized data.
- `.bss`: uninitialized data.
- `.rodata`: read-only data, when supported by the linker/script.

Labels:

```asm
loop_start:
    dec rcx
    jnz loop_start
```

A label does not generate instruction bytes. It only names an address.

Intel syntax:

```asm
mov rax, rbx    ; rax = rbx
add rax, 5      ; rax = rax + 5
```

Destination is on the left, source is on the right.
