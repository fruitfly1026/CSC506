# CSC/ECE 506 · Chapter 10 — Distributed Shared Memory Multiprocessors

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. How does a directory protocol scale better than broadcast/snoopy?
   - _Answer:_ The directory filters traffic: only the owner/sharer caches are contacted for a transaction. In broadcast, every cache controller participates.

2. Why can't the directory distinguish Exclusive from Modified?
   - _Answer:_ The cache's E→M transition is silent (no message). Without changing MESI, the directory can't tell them apart, so it keeps a single EM state.

3. Why is directory storage a scalability problem, and what mitigates it?
   - _Answer:_ Possible sharers grow with the number of caches → per-line bits grow → O(p²). Mitigations: coarse vector, limited pointers, sparse directory (the last two need an overflow policy).

4. What are the two sources of protocol races?
   - _Answer:_ Out-of-sync directory — the directory no longer reflects the caches' real states. Non-instantaneous processing — the home may overlap multiple transactions, so messages race.

5. What is the general strategy for dealing with protocol races?
   - _Answer:_ Add transient states when a transaction can't close immediately; NACK requests while in a transient state; and enlist nodes (outstanding-transaction buffers) to resolve the ambiguity.

6. How does a cache-based (SCI) directory store sharer information?
   - _Answer:_ As a doubly-linked list: the home holds only the head pointer; each sharing cache stores prev/next pointers. Storage is proportional to cache size, not p².

7. Why is write/invalidation latency O(sharers) in SCI?
   - _Answer:_ Invalidations must walk the list node by node — you can't reach the next sharer until you've processed the current one, so latency grows with the number of sharers.

8. State the central trade-off between memory-based and cache-based directories.
   - _Answer:_ Memory-based = O(1) inval latency, O(p²) storage. Cache-based = tiny storage, O(sharers) inval latency. Space vs. time.
