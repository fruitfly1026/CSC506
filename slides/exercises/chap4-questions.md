# CSC/ECE 506 · Chapter 4 — Parallel Programming for Linked Data Structures

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. Why can't we use `#pragma omp parallel for` to walk a linked list?
   - _Answer:_ Following `p = p->next` is a loop-carried dependence — the next address is unknown until the current node is dereferenced, so iterations aren't independent.

2. When does the structure-specific (tree) approach apply?
   - _Answer:_ Only when a node has out-degree > 1 (multiple child pointers), so independent subtrees can be searched in parallel.

3. State the serializability criterion.
   - _Answer:_ A parallel execution is correct if it produces a result identical to some sequential ordering of the same operations.

4. Name the three fine-grain locking hazards and one fix for each.
   - _Answer:_ Deadlock → global lock ordering (low→high). Dangling traversal → traversal locking (don't follow a node you don't hold). Deallocation → defer `free` / mark-and-GC, or traversal locking.

5. Why isn't a plain read lock enough in the "insert between Y and Z" case?
   - _Answer:_ P1 only needs Y to survive, not its value; a read lock still conflicts with P2's write on Y. A NoDelete lock (compatible with Write) removes the false conflict.

6. When is the among-readers strategy the right choice?
   - _Answer:_ When the structure is read-mostly — lookups vastly outnumber updates — so one read/write lock gives high concurrency with trivial code.
