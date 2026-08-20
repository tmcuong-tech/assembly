# Bits, Bytes, Words, and Number Bases

A bit is the smallest unit of information. It can only be `0` or `1`.

A byte is 8 bits. One byte can represent:

- Unsigned: 0 to 255.
- Signed 8-bit two's complement: -128 to 127.

Common x86/x86-64 sizes:

| Name | Bytes | Bits | NASM |
| --- | ---: | ---: | --- |
| byte | 1 | 8 | `db`, `resb` |
| word | 2 | 16 | `dw`, `resw` |
| dword | 4 | 32 | `dd`, `resd` |
| qword | 8 | 64 | `dq`, `resq` |

Binary often uses suffix `b`:

```asm
mov al, 10101010b
```

Hexadecimal is useful because 4 bits equal one hex digit:

```asm
mov al, 0A5h    ; MASM-style hex
mov al, 0xa5    ; common NASM/GAS-style hex
```

Signed and unsigned are interpretations. The stored bits are the same:

```text
11111111b = 255 as unsigned
11111111b = -1 as signed 8-bit
```

Two's complement:

- To negate an integer: invert the bits, then add 1.
- `neg ax` computes the two's complement of `ax`.

Endian order:

- x86 is little-endian.
- The word `1234h` is stored in RAM as low byte first: `34h`, then `12h`.
