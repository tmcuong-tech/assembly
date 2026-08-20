# GPU

A GPU was originally designed for graphics, but modern GPUs are also used for parallel computing.

CPU vs GPU:

- CPU: fewer powerful cores, good for complex control flow, branches, OS work, and general tasks.
- GPU: many smaller compute units, good for doing the same operation on many pieces of data.

Good GPU workloads:

- image and video processing;
- 2D/3D graphics;
- matrices, vectors, AI/ML;
- computations with many independent data items.

Poor GPU workloads:

- small amounts of data;
- heavy branching;
- very low-latency single-operation tasks;
- workloads that move data between CPU and GPU too often.

Main parts:

- Shader cores / compute units: parallel compute hardware.
- VRAM: GPU memory.
- Memory bandwidth: very important for graphics and compute.
- Driver: software layer connecting OS and GPU.

Normal x86 Assembly runs on the CPU, not the GPU. GPUs have their own instruction sets and are usually programmed through APIs such as CUDA, Vulkan, DirectX, or OpenCL.
