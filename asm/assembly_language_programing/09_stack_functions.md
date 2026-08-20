# Stack, Call, and Functions

The stack is memory used for return addresses, temporary values, and local variables. On x86-64, the stack usually grows downward toward lower addresses.

`push` and `pop`:

```asm
push rax    ; RSP = RSP - 8, [RSP] = RAX
pop rbx     ; RBX = [RSP], RSP = RSP + 8
```

`call` and `ret`:

```asm
call my_func
; CPU pushes the address of the next instruction, then jumps to my_func

my_func:
    ret
; CPU pops the return address into RIP
```

Simple function:

```asm
; input: RDI = a, RSI = b
; output: RAX = a + b
add_two:
    mov rax, rdi
    add rax, rsi
    ret
```

Calling it:

```asm
mov rdi, 10
mov rsi, 20
call add_two       ; RAX = 30
```

Basic stack frame:

```asm
my_func:
    push rbp
    mov rbp, rsp
    sub rsp, 16     ; reserve 16 bytes for locals

    ; body

    mov rsp, rbp
    pop rbp
    ret
```

A calling convention defines:

- where arguments are placed: registers or stack;
- which registers the caller must save and which the callee must restore;
- where the return value is placed.

Linux x86-64 System V typically uses `rdi`, `rsi`, `rdx`, `rcx`, `r8`, `r9` for C function arguments. Linux syscalls instead use `rdi`, `rsi`, `rdx`, `r10`, `r8`, `r9`.
