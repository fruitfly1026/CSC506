# CSC/ECE 506 · Chapter 1 — Perspectives on Parallel Architecture

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. What does Processor / CPU / Core mean in this course?
   - _Answer:_ Logic that can independently fetch and execute an instruction stream. It excludes caches.

2. State the low-hanging-fruit theory and how it explains the rise of multicore.
   - _Answer:_ Easy performance is taken first. ILP techniques were lower-hanging than multicore. Multicore needs TLP, and TLP needs parallel programming — so it came last, once ILP fruit ran out.

3. Using the theory, predict the future of multicore.
   - _Answer:_ Other approaches (e.g. specialization / accelerators) take over once parallel programming on multicore delivers diminishing returns.

4. Keep dynamic power constant with V, f fixed by shrinking die area. By how much?
   - _Answer:_ With S=0.7: 2× transistors at fixed V,f. To hold power constant, reduce area so the factor cancels → die area shrinks by ≈ 30% (1 − 1.4/2.0).

5. Difference between energy and power?
   - _Answer:_ Power is the rate of energy consumption (J/s = W).

6. Impact of threshold-voltage choice on static vs. dynamic power as transistors shrink?
   - _Answer:_ Lowering Vthd lets you lower V → dynamic power drops (≈linearly), but static/leakage power rises (exponentially).

7. How has processor design adapted to the power wall?
   - _Answer:_ Stalled frequency growth, went multicore, and added power management: clock gating, V/f scaling (DVFS), power gating.

8. Name the four categories of computers in Flynn's taxonomy.
   - _Answer:_ SISD, SIMD, MISD, MIMD.

9. Classify each system:
 
 
 - A single core in a multicore
 
 - GPU / Xeon-Phi-style co-processor
 
 - A multicore chip in a server
 
 - A server farm of cheap PCs
   - _Answer:_ single core → SISD · GPU/co-processor → SIMD (or SIMD/MIMD) · multicore chip → MIMD · server farm → distributed system (MIMD, no shared memory).
