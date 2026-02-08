# CAP Theorem

## 1. What Is CAP?
CAP is an acronym for three fundamental properties:

### Consistency (C)
All users see the same data at the same time.  
If data is written to Server A and read from Server B, it must return the latest value.

### Availability (A)
The system must always respond, even if there is a problem.  
The data may be old or new — the key point is that the server is not down.

### Partition Tolerance (P)
A partition is a network failure where servers cannot communicate.  
Partition tolerance means the system continues operating despite this failure.

---

## 2. The Golden Rule of CAP
In any distributed system, you can choose **only two out of the three**.  
Achieving all three at 100% is impossible.

Since network partitions are unavoidable in reality, **P is mandatory**, leaving a choice between:

- Consistency (C)
- Availability (A)

---

## 3. The Practical Scenario (Moment of Choice)
Imagine two nodes (Node 1 and Node 2) with a network partition between them:

- Data is updated on Node 1
- A user requests data from Node 2

The system has two options:

- **Reject the request (Error):**  
  Preserves Consistency → **CP system**

- **Return stale data:**  
  Preserves Availability → **AP system**

---

## 4. Real-World Examples

### Banking Systems
Must prioritize **Consistency**.  
Incorrect balances are unacceptable, so the system may become unavailable instead of returning wrong data.

### Social Media (Facebook / Twitter)
Prioritize **Availability**.  
If a post appears after a short delay, it’s acceptable as long as the platform is responsive.

---

## 5. System Types

### CP (Consistency + Partition Tolerance)
Examples: HBase, MongoDB (in certain configurations)  
Ensures accurate data but may become unavailable during network issues.

### AP (Availability + Partition Tolerance)
Examples: Cassandra, CouchDB  
Always responsive but may return stale data temporarily.

### CA (Consistency + Availability)
Exists only in single-node systems (e.g., standalone MySQL).  
Once data is distributed, CA becomes impossible.

---

## 6. Advanced Concepts Mentioned by Caleb
For deeper study as an AI or Backend Engineer:

- **Eventual Consistency**  
- **Quorums**  
- **Consensus Algorithms (Raft, Paxos)**

---

## Final Takeaway
CAP Theorem is about **trade-offs**:
- Need accuracy (banks)? Sacrifice availability.
- Need speed and uptime (social media)? Sacrifice immediate consistency.
