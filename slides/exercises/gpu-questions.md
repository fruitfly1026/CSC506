# CSC/ECE 506 · GPU Programming & Architecture

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. Why can a GPU use small caches yet still achieve high throughput?
   - _Answer:_ It hides memory latency with parallelism: while some warps wait on memory, the scheduler runs others, so the ALUs stay busy without needing big caches.

2. What does it mean to "hide" memory latency rather than reduce it?
   - _Answer:_ The memory is still slow (latency is not reduced); the GPU overlaps that wait with useful compute from other ready warps, so the stall is invisible to throughput.

3. How does SIMT differ from classic SIMD from the programmer's view?
   - _Answer:_ In SIMD you manage fixed-width vector lanes explicitly. In SIMT you write independent scalar threads, and the hardware implicitly groups 32 into a warp and runs them in lockstep.

4. Name three components inside an SM.   5. Why does the GPU's design only pay off for massively parallel problems?
   - _Answer:_ SM components: CUDA cores (ALUs), warp schedulers, register file, shared memory/L1. The design needs many independent threads to keep ~17,000 cores busy and to hide latency — serial/branchy work leaves them idle.

5. What are the responsibilities of the host vs. the device?
   - _Answer:_ Host (CPU): runs main, allocates device memory, copies data H2D/D2H, launches kernels. Device (GPU): runs kernels in parallel over thousands of threads on its own HBM memory.

6. What does the `__global__` qualifier mean?
   - _Answer:_ It marks a kernel: a function that runs on the GPU but is called (launched) from the CPU host.

7. Write the global-index expression and say why it's correct.   4. Why do we need `if (i < n)`?
   - _Answer:_ `i = blockIdx.x*blockDim.x + threadIdx.x`: blockIdx skips whole blocks of blockDim threads, threadIdx offsets within the block, giving a unique 0-based index. We launch ceil(n/256) blocks → a few extra threads, so the guard prevents out-of-bounds writes.

8. How do thread / block / grid map onto core / SM / whole-GPU?
   - _Answer:_ Thread → CUDA core; block → one SM (32-thread warps run in lockstep); grid → the whole GPU, spread across all SMs.

9. How many threads are in a warp, and how do they execute?
   - _Answer:_ 32 threads. They execute the same instruction each cycle in lockstep (SIMT), on different data.

10. What is branch divergence and when does it occur?
   - _Answer:_ When threads in the same warp take different control-flow paths. The warp serializes the paths (running each, masking the others), so a 2-way branch can cost up to 2×.

11. How does high occupancy help hide memory latency?
   - _Answer:_ More resident warps give the scheduler more ready work to issue while others stall on memory, so the SM's ALUs stay busy and the long memory latency is overlapped.

12. List the memory levels fastest→slowest.   5. What is coalescing?
   - _Answer:_ Registers → shared memory/L1 → L2 → global (HBM). Coalescing = when a warp's 32 threads hit consecutive addresses, the hardware merges them into one transaction; scattered accesses become many, so access pattern (data layout + indexing) matters enormously.

13. How does shared-memory tiling reduce global memory traffic?
   - _Answer:_ A block loads a tile from slow global memory into fast shared memory once, then all threads reuse it many times — fewer global accesses per FLOP, so higher arithmetic intensity.

14. What causes a shared-memory bank conflict?   3. Why does a parallel reduction take log₂(N) steps?
   - _Answer:_ A conflict happens when several threads in a warp access the same bank; those accesses serialize. A reduction pairs up partial results and halves the count each step, so N → 1 takes log₂(N) levels.

15. Give two reasons sparse SpMV is hard on a GPU.
   - _Answer:_ Any two of: uncoalesced/scattered access to nonzero columns; load imbalance from rows with different nonzero counts; branch divergence from variable-length row loops; low arithmetic intensity (memory-bound).

16. Which optimizations from this unit will you apply in Program 2?
   - _Answer:_ Choose a thread/block mapping that coalesces CSR-array access, use shared memory and reductions where rows are processed cooperatively, keep occupancy high, minimize divergence/imbalance, and minimize H2D/D2H copies — then measure against the sequential baseline.
