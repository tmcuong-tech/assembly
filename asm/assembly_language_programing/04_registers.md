# x86-64 Registers

A register is temporary storage inside the CPU.

General-purpose registers:

```text
RAX RBX RCX RDX RSI RDI RBP RSP
R8  R9  R10 R11 R12 R13 R14 R15
```

The same physical register has different names for different sizes:

```text
RAX: 64 bits
EAX: low 32 bits of RAX
AX : low 16 bits of RAX
AL : low 8 bits of AX
AH : high 8 bits of AX
```

Example:

```asm
mov rax, 0x1122334455667788
mov al, 0xff
; RAX becomes 0x11223344556677ff
```

Writing to a 32-bit register in x86-64 clears the upper 32 bits:

```asm
mov rax, -1      ; RAX = ffffffffffffffffh
mov eax, 5       ; RAX = 0000000000000005h
```

Common Linux syscall roles:

- `rax`: syscall number, return value.
- `rdi`: argument 1.
- `rsi`: argument 2.
- `rdx`: argument 3.
- `r10`: argument 4.
- `r8`: argument 5.
- `r9`: argument 6.

`rsp` is the stack pointer. If you corrupt `rsp`, the program may crash when `ret` tries to return to the wrong address.
