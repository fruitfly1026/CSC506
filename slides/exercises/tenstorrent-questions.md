# CSC/ECE 506 · Tenstorrent & TT-Metalium — Matmul Labs

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. Why does Tenstorrent have no cache hierarchy, and what replaces it?
   - _Answer:_ For dense tensor work the reuse pattern is known, so caches waste area/power and add coherence overhead. Instead the chip exposes large distributed L1 SRAM that any core can address over the NoC, with data movement scheduled explicitly by the program.

2. What are the five RISC-V cores and the three compute units in a Tensix core?
   - _Answer:_ RV 0 = reader, RV 4 = writer, RV 1–3 drive compute. The compute engine has the FPU (32×32 matrix), SFPU (vector), and ThCon (scalar / pack-unpack), plus ~1–1.5 MB L1 and two NoC routers.

3. What did Wormhole and Blackhole each add over Grayskull?
   - _Answer:_ Wormhole added 16 × 100 GbE ports for chip-to-chip scale-out (meshes / Galaxy). Blackhole moved to 6 nm and added 16 "big" RISC-V cores so the device manages more of its own data movement, cutting host round-trips.

4. Order the stack from hardware up, and say what each layer does.
   - _Answer:_ Hardware (Tensix grid) → TT-Metalium (bare-metal C++ kernels) → TT-NN (Python op library) → TT-Forge / TT-MLIR (compiles whole PyTorch/JAX/TF models down to Metalium). Runtime tools (TT-Inference-Server, TT-Studio) sit alongside for serving.

5. What dialects and passes does TT-MLIR use?
   - _Answer:_ Dialects TTIR → TTNN / TTKernel, with passes for operator fusion, sharding across cores, and layout/tiling selection, before lowering to TT-Metalium.

6. Why do the labs use raw TT-Metalium instead of TT-NN?
   - _Answer:_ To teach the hardware: at the Metalium level you must manage tiles, circular buffers, the NoC, and core placement by hand. Production users would typically use TT-NN or TT-Forge instead.

7. Why split the work into reader / compute / writer kernels?
   - _Answer:_ They map onto distinct RISC-V cores and run concurrently through circular buffers, overlapping DRAM movement with compute.

8. What tile indices feed one output tile `(mt,nt)`?
   - _Answer:_ A tiles `mt*Kt+kt` and B tiles `kt*Nt+nt` for `kt = 0…Kt-1`, accumulated by `matmul_tiles`.

9. How do we validate correctness with bf16 inputs?
   - _Answer:_ Untilize and compare to a CPU bf16 golden matmul using Pearson correlation, requiring > 0.97 rather than exact equality.

10. How does Tenstorrent SPMD scheduling differ from a GPU's?
   - _Answer:_ Work is assigned statically at launch — each core gets a fixed tile range with no dynamic scheduling, oversubscription, or work-stealing. An early-finishing core just idles.

11. Why does split_work_to_cores() return two core groups?
   - _Answer:_ To handle uneven splits: most cores do `work_per_core_1` tiles, a remainder group does `work_per_core_2`, so no per-core conditionals are needed at runtime.

12. What changes in the kernels vs. Lab 1?
   - _Answer:_ Each kernel takes a tile range (offset + count). The reader derives row/col by modulo, the compute outer loop is bounded by the count, and the writer offsets its output tile ids. The inner kt accumulation is unchanged.
