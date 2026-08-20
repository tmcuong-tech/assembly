# Assembly Learning Path

Learn Assembly like a programming language, but with an extra hardware layer.

Recommended order:

1. `00_introduction.md`: quick start, mental model, and first Windows/Linux run commands.
2. `01_introduction.md`: what Assembly is and how it differs from high-level languages.
3. `02_syntax_program_structure.md`: ASM syntax, sections, labels, comments.
4. `03_data_variables_memory.md`: variables, data sizes, byte/word/dword/qword allocation.
5. `04_registers.md`: x86-64 registers.
6. `05_operators_instructions.md`: common instructions and operations.
7. `06_flags_and_compare.md`: flags, `cmp`, `test`, signed vs unsigned.
8. `07_conditionals.md`: if/else/case using jumps.
9. `08_loops.md`: while/for/repeat using labels and jumps.
10. `09_stack_functions.md`: stack, call, ret, parameters.
11. `10_arrays_strings_addressing.md`: arrays, strings, addressing modes.
12. `11_macros_directives_build.md`: directives, macros, assemble/link workflow.
13. `12_examples_line_by_line.md`: examples explained line by line.

Notes:

- The repository contains both MASM 8086 material and NASM x86-64 material. These notes prioritize NASM/x86-64 because it matches modern machines, while mentioning MASM/8086 ideas when useful.
- In NASM, `;` starts a comment.
- Intel syntax uses `destination, source`: `mov rax, 5` means put 5 into `rax`.
