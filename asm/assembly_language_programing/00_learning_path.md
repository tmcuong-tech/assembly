# Assembly Learning Path

Learn Assembly like a programming language, but with an extra hardware layer.

Recommended order:

1. `01_introduction.md`: what Assembly is and how it differs from high-level languages.
2. `02_syntax_program_structure.md`: ASM syntax, sections, labels, comments.
3. `03_data_variables_memory.md`: variables, data sizes, byte/word/dword/qword allocation.
4. `04_registers.md`: x86-64 registers.
5. `05_operators_instructions.md`: common instructions and operations.
6. `06_flags_and_compare.md`: flags, `cmp`, `test`, signed vs unsigned.
7. `07_conditionals.md`: if/else/case using jumps.
8. `08_loops.md`: while/for/repeat using labels and jumps.
9. `09_stack_functions.md`: stack, call, ret, parameters.
10. `10_arrays_strings_addressing.md`: arrays, strings, addressing modes.
11. `11_macros_directives_build.md`: directives, macros, assemble/link workflow.
12. `12_examples_line_by_line.md`: examples explained line by line.

Notes:

- The repository contains both MASM 8086 material and NASM x86-64 material. These notes prioritize NASM/x86-64 because it matches modern machines, while mentioning MASM/8086 ideas when useful.
- In NASM, `;` starts a comment.
- Intel syntax uses `destination, source`: `mov rax, 5` means put 5 into `rax`.
