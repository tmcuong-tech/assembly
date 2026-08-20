# Conditions: if, else, and case

Assembly builds conditions with `cmp`/`test` and jump instructions.

If:

```c
if (rax < 0) rax = -rax;
```

```asm
cmp rax, 0
jge end_if          ; if rax >= 0, skip the body
neg rax
end_if:
```

If else:

```c
if (rax > rbx) rcx = rax;
else rcx = rbx;
```

```asm
cmp rax, rbx
jle else_part
mov rcx, rax
jmp end_if

else_part:
mov rcx, rbx

end_if:
```

AND condition:

```c
if (al >= 'A' && al <= 'Z') ...
```

```asm
cmp al, 'A'
jl end_if
cmp al, 'Z'
jg end_if
; then block
end_if:
```

OR condition:

```c
if (al == 'Y' || al == 'y') ...
```

```asm
cmp al, 'Y'
je then_block
cmp al, 'y'
je then_block
jmp end_if

then_block:
; then block

end_if:
```

Simple case:

```asm
cmp rax, 1
je case_1
cmp rax, 2
je case_2
jmp default_case
```
