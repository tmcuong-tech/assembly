# Common Operations and Instructions

Assembly does not use operators like `a + b` in C. It uses instructions.

Move data:

```asm
mov rax, 5          ; RAX = 5
mov rbx, rax        ; RBX = RAX
mov [value], rax    ; write RAX to RAM at value
mov rax, [value]    ; read RAM at value into RAX
xchg rax, rbx       ; swap RAX and RBX
```

Arithmetic:

```asm
add rax, rbx        ; RAX = RAX + RBX
sub rax, 10         ; RAX = RAX - 10
inc rcx             ; RCX = RCX + 1
dec rcx             ; RCX = RCX - 1
neg rax             ; RAX = -RAX
imul rbx            ; signed multiply
mul rbx             ; unsigned multiply
idiv rbx            ; signed divide
div rbx             ; unsigned divide
```

Bitwise logic:

```asm
and al, 0Fh         ; keep low 4 bits
or  al, 80h         ; set bit 7
xor al, 20h         ; toggle bit 5
not al              ; invert all bits
```

Shift and rotate:

```asm
shl rax, 1          ; shift left, roughly multiply by 2
shr rax, 1          ; logical right shift, unsigned divide by 2
sar rax, 1          ; arithmetic right shift, keeps signed sign bit
rol al, 1           ; rotate left
ror al, 1           ; rotate right
```

Address calculation:

```asm
lea rax, [rbx + rcx*4 + 8] ; compute address, do not read RAM
```

Important notes:

- x86 generally does not allow memory-to-memory operations such as `mov [a], [b]`. Use a register in between.
- Operands must have compatible sizes.
- `lea` computes an address; `mov rax, [addr]` reads memory.
