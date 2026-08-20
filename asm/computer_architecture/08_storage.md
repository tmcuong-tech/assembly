# External Storage: HDD, SSD, and Files

Storage keeps data after power is off. Unlike RAM, storage is persistent.

HDD:

- Uses spinning magnetic platters and moving heads.
- Slower than SSD because it has mechanical movement.
- Good for large, cheaper capacity.

SSD:

- Uses flash memory.
- Faster than HDD and has lower latency.
- Has limited write cycles, so the controller performs wear leveling.

Why Assembly programs do not usually read files with raw CPU instructions:

- CPUs have low-level I/O mechanisms, but modern user programs are not allowed to access devices directly.
- Programs call the operating system through syscalls/APIs.
- The OS and drivers handle filesystems, caches, controllers, and devices.

Path of a file read:

1. Program calls syscall `read`.
2. OS checks permissions and the file descriptor.
3. Filesystem locates storage blocks.
4. Driver/controller transfers data.
5. Data is placed in kernel memory and copied or mapped into the program.
