# Line-by-Line Examples

## Creating a variable and checking its size

```asm
section .data
age db 25
```

Explanation:

- `section .data`: starts the initialized data section.
- `age`: a label, the name of the first byte's address.
- `db`: define byte.
- `25`: initial value.
- Result: allocates 1 byte = 8 bits. If `age` is at address 0x1000, byte 0x1000 stores value 25.

```asm
score dw 1000
```

- `dw`: define word.
- Allocates 2 bytes = 16 bits.
- On little-endian x86, decimal 1000 = 03E8h, so RAM stores low byte `E8h` first, then high byte `03h`.

```asm
items resd 10
```

- `resd`: reserve doubleword.
- Each element is 4 bytes = 32 bits.
- 10 elements = 40 bytes = 320 bits.
- Usually placed in `.bss`, meaning the source reserves space without storing initial values.

## Hello world on Linux x86-64

```asm
bits 64

section .text
global _start

_start:
    mov rax, 1
    mov rdi, 1
    mov rsi, msg
    mov rdx, msg.len
    syscall

    mov rax, 60
    mov rdi, 0
    syscall

section .data
msg: db "Hello, world!", 10
.len: equ $ - msg
```

Line-by-line:

- `bits 64`: tell the assembler to generate 64-bit instructions.
- `section .text`: code section.
- `global _start`: export `_start` so the linker can use it as the entry point.
- `_start:`: program start address.
- `mov rax, 1`: Linux syscall number 1 is `write`.
- `mov rdi, 1`: argument 1, file descriptor 1 means stdout.
- `mov rsi, msg`: argument 2, address of the string.
- `mov rdx, msg.len`: argument 3, number of bytes to write.
- `syscall`: enter the kernel to execute `write`.
- `mov rax, 60`: Linux syscall number 60 is `exit`.
- `mov rdi, 0`: exit code 0.
- `syscall`: terminate the program.
- `section .data`: initialized data section.
- `msg: db "Hello, world!", 10`: allocates 14 bytes: 13 characters plus newline.
- `.len: equ $ - msg`: computes string length as current position minus address of `msg`.

## Signed if

```asm
cmp rax, 0
jge not_negative
neg rax
not_negative:
```

- `cmp rax, 0`: sets flags based on `rax - 0`.
- `jge`: jump if signed greater-or-equal, meaning `rax >= 0`.
- `neg rax`: only runs when `rax < 0`, turning it positive.

## Array access

```asm
section .data
nums dd 10, 20, 30

section .text
mov rcx, 1
mov eax, [nums + rcx*4]
```

- `nums dd 10, 20, 30`: 3 elements, each 4 bytes, total 12 bytes.
- `mov rcx, 1`: index = 1.
- `[nums + rcx*4]`: address = start of array + 1 * 4.
- `mov eax, ...`: reads the second element, value 20, into `eax`.
