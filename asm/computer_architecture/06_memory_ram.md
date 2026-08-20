# RAM and Memory

RAM can be viewed as a very large array of bytes. Every byte has its own address.

Example:

```text
Address: 1000 1001 1002 1003
Data:      2A   45   B8   20
```

If `x db 2Ah` is placed at address 1000, then `x` is a name for address 1000.

A process usually has these memory regions:

- `.text`: machine code, usually read-only and executable.
- `.rodata`: read-only constants.
- `.data`: initialized global/static data.
- `.bss`: uninitialized global/static data, allocated and usually zeroed by the loader.
- heap: dynamically allocated memory, usually grows upward.
- stack: function calls and local storage, usually grows downward.

Stack:

- `push rax`: decreases `rsp`, then writes 8 bytes from `rax` to the stack.
- `pop rax`: reads 8 bytes from the stack into `rax`, then increases `rsp`.
- `call label`: pushes the return address, then jumps to `label`.
- `ret`: pops a return address into `rip`.

Common mistakes:

- Reading the wrong size, such as reading a `word` from a 1-byte variable.
- Forgetting `[]`: `mov rax, x` loads an address/label value; `mov rax, [x]` reads data at address `x`.
- Writing to `.text` or `.rodata`, causing a memory protection fault.
