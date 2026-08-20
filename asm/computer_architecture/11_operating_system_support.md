# Operating System Support

The operating system lets user programs run safely and share hardware resources.

The OS provides:

- processes and threads;
- memory management;
- filesystems;
- device drivers;
- syscalls/APIs;
- access protection;
- a scheduler that decides what runs next.

Virtual memory:

- Each process appears to have its own address space.
- The address seen by the program is a virtual address.
- The MMU translates virtual addresses to physical addresses.
- Page tables store address mappings.
- The TLB caches recent address translations.

Page fault:

- Happens when a page is missing from RAM or access violates permissions.
- The OS may load a page, allocate a new page, or terminate the program.

Loader:

- Reads the executable file.
- Loads `.text`, `.data`, `.rodata`, and allocates `.bss`.
- Prepares stack, arguments, and environment.
- Transfers control to the entry point, such as `_start`.

Privilege:

- User mode: normal programs, limited hardware access.
- Kernel mode: OS/drivers, high privilege.
- A syscall is a controlled transition from user mode to kernel mode.
