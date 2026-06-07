# CSC/ECE 506 · Chapter 5 — Introduction to Memory Hierarchy Organization

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. In a 4-way cache, what do "set", "way", and "line" mean?
   - _Answer:_ A set is a row selected by the index; a way is one of the 4 columns; a line is a single cell (one block's worth of storage).

2. For 2048 sets and 64-byte blocks, how many offset and index bits?
   - _Answer:_ 6 offset bits (\(2^6=64\)) and 11 index bits (\(2^{11}=2048\)); the remaining high bits are the tag.

3. Why is pseudo-LRU preferred to true LRU in big caches?
   - _Answer:_ True LRU costs \(O(\text{ways}^2)\) state; pseudo-LRU is \(O(\text{ways})\) and tracks recency well enough.

4. Why does inclusion simplify handling an external coherence request?
   - _Answer:_ You only check the lower level. If the block isn't there, the upper level can't have it — so the upper level's tags aren't disturbed.

5. In VIPT, why can the cache start the lookup before translation finishes?
   - _Answer:_ The page-offset bits are identical in VA and PA, so the index (taken from them) is available immediately; the TLB supplies the physical tag in parallel.

6. Which "C" does more associativity reduce, and which does a bigger cache reduce?
   - _Answer:_ More associativity → fewer conflict misses; bigger cache → fewer capacity misses.

7. Distinguish physical from logical cache organization.
   - _Answer:_ Physical = how cores connect to cache parts (united / distributed / hybrid). Logical = who may fill a part (private / shared). They are independent axes.

8. Shared distributed caches have the worst what, and how is it fixed?
   - _Answer:_ Worst distance locality (data far away). Fixed by victim replication — keep evicted remote blocks in the local tile.

9. Private caches have the worst what, and how is it fixed?
   - _Answer:_ Worst fragmentation (wasted capacity). Fixed by capacity sharing — spill victims into remote caches with free space.
