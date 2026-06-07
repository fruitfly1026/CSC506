# CSC/ECE 506 · Chapter 8 — Hardware Support for Synchronization

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. What is the purpose of an atomic RMW instruction?
   - _Answer:_ It is the hardware primitive that lets software build all higher-level synchronization (locks, barriers, semaphores).

2. What factors matter when implementing a lock?
   - _Answer:_ Uncontended latency, traffic scalability (on release and on failed attempts), fairness, and storage overhead.

3. What does TTSL improve over test&set?
   - _Answer:_ It spins on reads, so no invalidations are generated while the lock is held.

4. What does LL/SC improve over TTSL?
   - _Answer:_ A failed lock acquisition (failed SC) generates no bus transaction.

5. What problem does the ticket lock improve over LL/SC?
   - _Answer:_ Fairness: a thread that wants the lock is guaranteed to eventually get it (FIFO queue order).

6. What problem does ABQL improve over the ticket lock?
   - _Answer:_ Traffic: a release invalidates only one sharer (the next in line) instead of all sharers — O(1) instead of O(p).

7. What hardware support is needed for HTM?
   - _Answer:_ Speculative-state buffering, conflict detection, a commit mechanism, and a rollback mechanism.
