# Cache Memory

Cache is small, very fast memory close to the CPU. Its purpose is to reduce how often the CPU must wait for RAM.

Typical speed hierarchy:

1. Registers: fastest and smallest.
2. L1 cache: very fast, usually per core.
3. L2 cache: larger than L1, slower than L1.
4. L3 cache: larger, often shared by cores.
5. RAM: large but slower than cache.
6. SSD/HDD: much larger but far slower than RAM.

Locality:

- Temporal locality: data used recently is likely to be used again soon.
- Spatial locality: data near recently used data is likely to be used soon.

Array example:

```c
for (i = 0; i < n; i++) sum += a[i];
```

Sequential access is cache-friendly because nearby elements are stored close together in RAM.

Cache line:

- The CPU usually does not load one byte at a time from RAM into cache.
- It loads a block called a cache line.
- Sequential access can reuse data already brought in by the same cache line.

In Assembly, data layout and loop order can strongly affect cache performance.
