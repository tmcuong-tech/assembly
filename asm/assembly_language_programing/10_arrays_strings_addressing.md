# Arrays, Strings, and Addressing Modes

An addressing mode tells the CPU how to compute a memory address.

Immediate:

```asm
mov rax, 10         ; 10 is a constant
```

Register:

```asm
mov rax, rbx        ; data is in a register
```

Direct memory:

```asm
mov al, [age]       ; read byte at label age
```

Indirect:

```asm
mov rbx, age
mov al, [rbx]       ; RBX contains the address
```

Base + displacement:

```asm
mov rax, [rbx + 24]
```

Base + index * scale + displacement:

```asm
mov eax, [array + rcx*4]
mov eax, [rbx + rcx*4 + 8]
```

Valid x86 scale values: 1, 2, 4, 8.

Arrays:

```asm
bytes db 1, 2, 3        ; each element is 1 byte
words dw 100, 200       ; each element is 2 bytes
dnums dd 10, 20, 30     ; each element is 4 bytes
qnums dq 1, 2           ; each element is 8 bytes
```

Accessing elements:

```asm
mov al,  [bytes + rcx]      ; byte index
mov ax,  [words + rcx*2]    ; word index
mov eax, [dnums + rcx*4]    ; dword index
mov rax, [qnums + rcx*8]    ; qword index
```

C-style string ending with byte 0:

```asm
msg db "hello", 0
```

A string for syscall `write` does not need byte 0, but it does need a length:

```asm
msg db "hello", 10
msg_len equ $ - msg
```
