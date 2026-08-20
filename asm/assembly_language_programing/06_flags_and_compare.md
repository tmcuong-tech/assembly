# Flags, Comparison, and Signed/Unsigned Logic

Flags are status bits in the flags register. Many arithmetic and logic instructions update them.

Important flags:

- `ZF`: Zero Flag, set when the result is zero.
- `SF`: Sign Flag, set from the top bit of the result.
- `CF`: Carry Flag, used for unsigned carry/borrow.
- `OF`: Overflow Flag, used for signed overflow.

`cmp`:

```asm
cmp rax, rbx
```

The CPU internally computes `rax - rbx`, sets flags, and discards the result. `rax` and `rbx` are not changed.

`test`:

```asm
test rax, rax
```

The CPU internally computes `rax AND rax`, sets flags, and discards the result. This is commonly used to test whether a value is zero.

Equality jumps:

```asm
cmp rax, 10
je  equal       ; ZF=1
jne not_equal   ; ZF=0
```

Unsigned jumps:

```asm
cmp rax, rbx
ja  above       ; rax > rbx unsigned
jae above_eq
jb  below
jbe below_eq
```

Signed jumps:

```asm
cmp rax, rbx
jg  greater     ; rax > rbx signed
jge greater_eq
jl  less
jle less_eq
```

Using the wrong signed/unsigned jump gives wrong logic:

```text
0xff = 255 as unsigned
0xff = -1 as signed 8-bit
```

Use unsigned comparisons for sizes, lengths, counts, and addresses. Use signed comparisons for values that can be negative.
