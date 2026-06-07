# CSC/ECE 506 · Chapter 2 — Perspectives on Parallel Programming

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. What is a programming model, and which two dominate multiprocessors?
   - _Answer:_ An abstraction the hardware provides to the programmer. The two dominant ones are
 shared memory and message passing.

2. How does each model communicate and synchronize?
   - _Answer:_ Shared memory: implicit communication through loads/stores, with
 explicit synchronization. Message passing: explicit communication via send/recv,
 which automatically synchronizes.

3. Why is the thread/process analogy useful here?
   - _Answer:_ Threads share the address space (≈ shared memory); processes share nothing
 (≈ message passing). The uniprocessor concepts map directly onto the two models.

4. What primitives does shared-memory parallel programming require?
   - _Answer:_ Variable scope (shared vs. private) and synchronization
 primitives — locks and barriers.

5. How does the reduction differ between the two models?
   - _Answer:_ Shared memory: a single shared `sum` guarded by a lock.
 Message passing: each worker computes a local sum, then partials are gathered by messages.

6. Why is shared memory easy to develop but hard to tune?
   - _Answer:_ It hides data layout and communication (easy to write), but those same hidden details
 — layout, communication pattern, topology — must be tuned for scalability.

7. What are the two basic parallel programming models?
   - _Answer:_ Shared memory and message passing.

8. Key advantages and disadvantages of shared memory over message passing?
   - _Answer:_ Pluses: implicit communication, lower development effort, finer-grained
 communication. Minuses: explicit synchronization, higher tuning effort, requires hardware support.

9. How does transactional memory simplify parallel programming?
   - _Answer:_ Higher abstraction (simpler coding and reasoning) and it removes lock-related problems —
 no explicit locks, no deadlocks.
