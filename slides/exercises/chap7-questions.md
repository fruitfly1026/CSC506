# CSC/ECE 506 · Chapter 7 — Bus-Based Cache Coherence

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. What is a bus, and what properties make it attractive for a small-scale multiprocessor?
   - _Answer:_ A set of long shared wires with arbitration. It is simple, cheap, and extendable — you can plug in more processors as needed. But clock skew limits its scalability.

2. What components are needed to build a bus-based multiprocessor?
   - _Answer:_ Snoopers (at each processor and at memory), plus modifications to the cache controller, tag array, and its FSM — additional states and state transitions for coherence.

3. What does the memory controller do?
   - _Answer:_ On snooped BusRd or BusRdX → read and supply data (unless a cache Flushes first). On snooped Flush → update main memory.

4. On a BusRdX, if the block is M, why Flush it — we're about to overwrite it anyway?
   - _Answer:_ Writes may target different words within the block, so we must fetch the latest copy first. Also, BusRdX signals intent to write, but a read of the block may still follow.

5. Writing to a block already Shared — what's more efficient than BusRdX?
   - _Answer:_ BusUpgr: the cache already has valid data, so it only needs to invalidate peers — no data transfer required.

6. Contrast the two protocols in this module: write-through and MSI.
   - _Answer:_ Write-through coherence is for write-through caches; MSI is for write-back caches (write hits stay in the cache, cutting bus traffic).

7. When is a written value propagated?
   - _Answer:_ Step 1: a write invalidates other cached copies. Step 2: a later read by a peer misses and reloads the new value — from memory (write-through) or from the peer cache that wrote it (MSI).

8. How does MESI improve on MSI?
   - _Answer:_ A block that is read then written incurs only one bus transaction (not two), thanks to the Exclusive state — E → M is silent.

9. What assumption underlies cache-to-cache transfer in MESI?
   - _Answer:_ That a peer cache can supply the block faster than outer memory. Not always true — hence FlushOpt is optional.

10. How does MOESI improve on MESI?
   - _Answer:_ Dirty sharing: a dirty block may be shared as long as one cache keeps it in the Owner state, reducing Flushes to main memory.

11. How does Dragon differ from MSI / MESI / MOESI?
   - _Answer:_ Dragon uses write update: a written value is immediately propagated to peer caches (BusUpd), rather than invalidating them.

12. What is a coherence miss, and what are its two types?
   - _Answer:_ A miss caused by a block being invalidated when a peer wrote it (only in invalidation protocols). Two types: true sharing (real read/write sharing) and false sharing (different bytes/words co-located in one block).

13. How is a write value propagated in multi-level caches?
   - _Answer:_ First downstream (write-through or write-notification to L2), then upstream (invalidate any caches that may hold the block).
