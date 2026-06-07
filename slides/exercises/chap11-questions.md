# CSC/ECE 506 · Chapter 11 — Interconnection Networks

In-class review questions — **ungraded / formative**. Paste into a Google Form (one form per chapter).
Reference answers are for the instructor; omit them from the student form.

1. Describe stop/go flow control.
   - _Answer:_ A link-level scheme: the destination router sends a stop or go signal to the source router depending on the destination's buffer level; the source pauses or resumes flits accordingly.

2. What metrics characterize a network topology?
   - _Answer:_ Diameter, average distance, bisection bandwidth, number of links, and degree of connection.

3. Packet vs. circuit switching — better and worse?
   - _Answer:_ Better: easier to maximize link utilization, no connection setup. Worse: larger buffers, higher and less predictable latency, higher per-packet overheads.

4. Sort by routing-table area: adaptive source, dimension-ordered, adaptive per-hop.
   - _Answer:_ Adaptive source (largest) > adaptive per-hop (smaller) > dimension-ordered (zero).

5. What principle underlies deadlock-free routing? Name a few schemes.
   - _Answer:_ Cyclic channel acquisition creates the possibility of deadlock — break the cycles. Examples: dimension-ordered routing, turn restriction (west-first / north-last), and up*/down* routing.

6. How can a virtual channel be used to escape a deadlock?
   - _Answer:_ A regular VC (deadlock possible) is used first; an escape VC (provably deadlock-free) is used upon congestion, guaranteeing forward progress.
