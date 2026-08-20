# Data, Variables, and Memory

In Assembly, a variable is a name attached to a region of bytes in memory.

Initialized data:

```asm
section .data
age     db 25       ; 1 byte = 8 bits
score   dw 1000     ; 2 bytes = 16 bits
count   dd 123456   ; 4 bytes = 32 bits
total   dq 0        ; 8 bytes = 64 bits
msg     db "Hi", 10 ; 3 bytes: 'H', 'i', newline
```

Uninitialized data:

```asm
section .bss
buffer  resb 64     ; reserve 64 bytes
items   resd 10     ; reserve 10 dwords = 40 bytes = 320 bits
value   resq 1      ; reserve 1 qword = 8 bytes = 64 bits
```

Size table:

| Directive | Meaning | Allocation |
| --- | --- | --- |
| `db` / `resb` | byte | 1 byte = 8 bits |
| `dw` / `resw` | word | 2 bytes = 16 bits |
| `dd` / `resd` | dword | 4 bytes = 32 bits |
| `dq` / `resq` | qword | 8 bytes = 64 bits |

Reading values and loading addresses:

```asm
mov al, [age]       ; read 1 byte at address age into AL
mov rax, age        ; load the address of age into RAX
mov rax, [total]    ; read 8 bytes at address total into RAX
```

Writing values:

```asm
mov byte [age], 26
mov qword [total], 500
```

Specify size when the assembler cannot infer it:

```asm
mov [age], 26       ; ambiguous: 1, 2, 4, or 8 bytes?
mov byte [age], 26  ; clear: write 1 byte
```

Arrays:

```asm
nums dd 10, 20, 30
; nums     is the first element, 4 bytes
; nums+4   is the second element
; nums+8   is the third element
```
