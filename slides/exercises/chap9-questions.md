# CSC/ECE 506 · Chapter 9 — Memory Consistency Models

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. What two expectations do programmers have when writing a parallel program?
   - _Answer:_ Program order — accesses appear in source-code order; and atomicity — each access happens all-at-once with respect to every processor.

2. Name two optimizations that speed up a sequentially consistent machine.
   - _Answer:_ Prefetching (read and exclusive/write prefetch) and load speculation (with cancel-and-replay on invalidation).

3. Which ordering does Processor Consistency relax?
   - _Answer:_ Store → Load. Loads need not wait for older stores; it also drops write atomicity.

4. What ordering is relaxed, and what is imposed, by Weak Ordering?
   - _Answer:_ Relaxed: any ld/st → ld/st ordering. Imposed: synch → ld/st and ld/st → synch.

5. How does Release Consistency improve on Weak Ordering?
   - _Answer:_ It splits synch into acquire and release, and so allows overlapped execution of critical sections.

6. What migration is prevented by a regular fence, an acquire, and a release?
   - _Answer:_ Regular fence → both directions. Acquire → upward migration. Release → downward migration.
