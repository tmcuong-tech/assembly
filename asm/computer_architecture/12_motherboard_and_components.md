# Computer Components

CPU:

- Executes machine instructions.
- Contains registers, ALU, control unit, and cache.
- Connects to RAM and devices through platform interconnects.

RAM:

- Stores programs and data currently in use.
- Loses contents when power is off.
- Faster than storage, slower than cache/registers.

Motherboard:

- Main circuit board connecting CPU, RAM, storage, GPU, USB, network, and audio.
- Provides RAM slots, PCIe slots, CPU socket, and power connectors.

Chipset / platform controller:

- Manages many I/O connections.
- In modern systems, some old chipset roles, such as the memory controller, are inside the CPU.

GPU:

- Handles graphics and parallel computation.
- Can be integrated into the CPU or installed as a discrete PCIe card.

Storage:

- SSD/HDD stores OS, programs, and files.
- NVMe SSDs use PCIe and are faster than SATA SSDs.

PSU:

- Power supply unit converts AC power into DC rails for components.
- Must provide enough stable power.

Cooling:

- Removes heat from CPU/GPU.
- If too hot, CPU/GPU may reduce clock speed or shut down to protect hardware.

Network adapter:

- Provides Ethernet/Wi-Fi networking.
- Uses drivers and may use DMA to move packets into RAM.

BIOS/UEFI:

- Firmware that starts the machine.
- Checks hardware, selects boot device, and loads the bootloader.

Display, keyboard, mouse, and audio:

- I/O devices.
- Applications normally access them through OS APIs, not by controlling hardware directly.
