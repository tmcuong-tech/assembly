# Loops

A loop in Assembly is a label plus a jump.

While:

```c
while (rcx != 0) {
    rcx--;
}
```

```asm
while_start:
    cmp rcx, 0
    je while_end
    dec rcx
    jmp while_start
while_end:
```

Do while / repeat until:

```asm
repeat_start:
    ; body runs at least once
    dec rcx
    cmp rcx, 0
    jne repeat_start
```

For with a counter:

```c
for (i = 0; i < 10; i++) ...
```

```asm
xor rcx, rcx        ; i = 0
for_start:
    cmp rcx, 10
    jge for_end
    ; body
    inc rcx
    jmp for_start
for_end:
```

The `loop` instruction:

```asm
mov rcx, 10
top:
    ; body
    loop top        ; decrement RCX, jump if RCX != 0
```

Be careful: if the counter starts at 0, `loop` can run many times because the counter underflows.

Iterating over a dword array:

```asm
section .data
nums dd 10, 20, 30

section .text
mov rbx, nums       ; address of first element
xor rcx, rcx        ; index = 0

loop_nums:
    cmp rcx, 3
    jge done
    mov eax, [rbx + rcx*4]  ; each dd element is 4 bytes
    inc rcx
    jmp loop_nums
done:
```
