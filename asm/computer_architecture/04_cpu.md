# CPU

The CPU is the central processing unit. It executes machine instructions.

Main parts:

- ALU: arithmetic and logic operations such as `add`, `sub`, `and`, `or`, `xor`.
- Control Unit: controls fetch, decode, execute, and internal CPU coordination.
- Registers: extremely fast storage inside the CPU.
- Instruction decoder: translates opcodes into internal operations.
- Execution units: hardware blocks that perform instructions, often in parallel.
- Memory unit: handles memory reads/writes, cache, and TLB interaction.

The CPU does not understand high-level variables. It sees:

- registers;
- memory addresses;
- immediate constants;
- machine instructions.

Pipeline:

- Instead of finishing one instruction before starting the next, the CPU splits execution into stages.
- Multiple instructions can be in different pipeline stages at the same time.
- Branch prediction guesses the next path so the pipeline can stay busy.

RISC and CISC:

- RISC uses a smaller, simpler, more regular instruction set.
- CISC, such as x86, has more complex instructions and can often operate on memory directly.
- Modern x86 CPUs internally break complex instructions into smaller micro-operations.
