# How a Computer Works

A computer runs a program by repeating the instruction cycle:

1. Fetch: the CPU reads an instruction from memory at the address in the instruction pointer.
2. Decode: the CPU decodes the instruction to know what operation to perform.
3. Execute: the CPU performs the operation, reads/writes registers, reads/writes RAM, or jumps to another address.
4. Update: the CPU updates the instruction pointer and flags when needed.

Example:

```asm
mov rax, 5      ; load 5 into RAX
add rax, 3      ; RAX = 8
cmp rax, 8      ; compare RAX with 8, sets ZF=1
je equal        ; jump to equal if ZF=1
```

The CPU does not understand high-level `if` statements. It understands:

- compare values and set flags;
- test flags;
- change the next instruction address if a condition is true.

The instruction cycle is synchronized by a clock:

- A clock is the hardware timing signal.
- 3 GHz means 3 billion cycles per second, but one instruction does not always equal one cycle.
- Cache misses, RAM access, wrong branch prediction, and I/O can make the CPU wait.

A computer is fast when CPU, cache, RAM, buses, storage, operating system, and program behavior work well together.
