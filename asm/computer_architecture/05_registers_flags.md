# Registers and Flags

Registers are extremely fast storage locations inside the CPU. Assembly uses registers constantly because register access is much faster than RAM access.

Common x86-64 general-purpose registers:

| 64-bit | 32-bit | 16-bit | Low 8-bit | Common role |
| --- | --- | --- | --- | --- |
| `rax` | `eax` | `ax` | `al` | result, syscall number |
| `rbx` | `ebx` | `bx` | `bl` | temporary data |
| `rcx` | `ecx` | `cx` | `cl` | counter, shift count |
| `rdx` | `edx` | `dx` | `dl` | multiply/divide extension, argument |
| `rsi` | `esi` | `si` | `sil` | source index, argument |
| `rdi` | `edi` | `di` | `dil` | destination index, argument |
| `rsp` | `esp` | `sp` | `spl` | stack pointer |
| `rbp` | `ebp` | `bp` | `bpl` | frame pointer |
| `rip` | | | | instruction pointer |

Flags in `RFLAGS` describe the result of recent operations:

| Flag | Name | Meaning |
| --- | --- | --- |
| `ZF` | Zero Flag | result is zero |
| `SF` | Sign Flag | top bit of result is 1 |
| `CF` | Carry Flag | unsigned carry/borrow |
| `OF` | Overflow Flag | signed overflow |
| `PF` | Parity Flag | low byte has an even number of 1 bits |
| `DF` | Direction Flag | direction for string instructions |

Example:

```asm
mov al, 255
add al, 1       ; AL = 0, CF=1, ZF=1

mov al, 127
add al, 1       ; AL = 128, OF=1 if interpreted as signed 8-bit
```

`cmp a, b` internally computes `a - b` to set flags, but it does not store the result.

`test a, b` internally computes `a AND b` to set flags, but it does not store the result.
