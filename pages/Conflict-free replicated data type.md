
Conflict-free replicated data type([[CRDT]])


- operation-based CRDTs
- state-based CRDTs
- > State-based CRDTs are often simpler to design and to implement; their only requirement from the communication substrate is some kind of [[gossip protocol]].
- > State-based CRDTs are called convergent replicated data types, or CvRDTs. In contrast to CmRDTs, CvRDTs send their full local state to other replicas, where the states are merged by a function which must be [[commutative]], [[associative]], and [[idempotent]]. The merge function provides a join for any pair of replica states, so the set of all states forms a semilattice. The update function must monotonically increase the internal state, according to the same partial order rules as the semilattice.
- > Sequence CRDTs
    - >  A sequence, list, or ordered set CRDT can be used to build a [[Collaborative real-time editor]], as an alternative to [[Operational transformation]] (OT).
    - > [[LogootSplit]] was proposed as an extension of Logoot in order to reduce the metadata for sequence CRDTs.
