# CSC/ECE 506 · Chapter 3 — Shared Memory Parallel Programming

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. What are the three types of dependences?
   - _Answer:_ True (producer→consumer, RAW), anti (WAR), and output (WAW).

2. Which dependence types are tied to loop structure?
   - _Answer:_ Loop-carried (across iterations) and loop-independent (within one iteration). Only loop-carried dependences block iteration-level parallelism.

3. ITG vs. LDG — what does each show?
   - _Answer:_ The ITG shows the traversal (happens-before) order; the LDG shows the actual dependences between iteration points.

4. Describe DOALL, DOACROSS, function, and DOPIPE parallelism.
   - _Answer:_ - DOALL — parallelism between independent loop iterations.
 
 - DOACROSS — parallelism between dependent iterations, guarded by synchronization.
 
 - Function — parallelism between independent code sections (e.g. distributed loops).
 
 - DOPIPE — parallelism between dependent statements in a loop, software-pipelined with synchronization.

5. Define the main variable scopes in shared-memory parallel programming.
   - _Answer:_ Shared — all threads see one copy. Private — each thread has its own copy (OpenMP refines into `firstprivate`/`lastprivate`). Reduction — private partials merged by a commutative/associative operator.

6. Parallelizing the `for j` loop of a nest with arrays A,B,C,Y and scalars x,k — give the scopes.
   - _Answer:_ Shared: `i, n, m, A, B, C, Y`   Private: `j, k, x`.

7. What synchronization primitives does a shared-memory system support?
   - _Answer:_ Lock (mutual exclusion), barrier (global event), and point-to-point (e.g. post/wait).

8. Why is load balancing important when barriers are used?
   - _Answer:_ A parallel region's execution time is determined by the slowest thread — imbalance leaves everyone else idle at the barrier.

9. What does gang scheduling solve — and not solve?
   - _Answer:_ It prevents the no-forward-progress stall when a thread is switched out, and frees CPUs for other work during a switch-out. It does not remove inherent load imbalance.
