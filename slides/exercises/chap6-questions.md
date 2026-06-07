# CSC/ECE 506 · Chapter 6 — Introduction to Shared Memory Multiprocessors

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. Do P1 and P2 see the same value of `sum` at the end?
   - _Answer:_ No — each holds its own private copy; without a coherence protocol they diverge.

2. What if we use write-through caches instead of write-back?
   - _Answer:_ Still broken. Writes reach memory immediately, but the other cache keeps its stale copy
 until it is told to update or invalidate. Propagation is still missing.

3. What if there are no caches, or `sum` is uncachable?
   - _Answer:_ Then it works — every access goes straight to the single shared memory location. But giving up
 caching destroys performance, so we keep caches and add a protocol.

4. What two principles define cache coherence?
   - _Answer:_ Write propagation (a write reaches all caches) and
 write serialization (all processors see writes to one address in the same order).

5. How does memory consistency differ from coherence?
   - _Answer:_ Coherence orders accesses to a single address; the
 consistency model defines ordering guarantees across different addresses.

6. Why does the naïve spin lock fail, and what fixes it?
   - _Answer:_ Its test-then-set isn't atomic, so two threads can both acquire. A hardware
 atomic instruction (atomic load–modify–store) fixes it.

7. What key concepts do we need to support the shared-memory abstraction in multiprocessors?
