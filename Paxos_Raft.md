# Consensus Algorithms: Paxos vs Raft

## 1. Paxos — “The Complex Founding Father”
Paxos is the first successful algorithm to solve the **Consensus** problem.  
It appeared in the 1990s and was introduced by **Leslie Lamport**.

### Philosophy
It is based on a **role-based model**:
- Proposer
- Acceptor
- Learner

### How It Works
The protocol operates in **two phases**:

**Prepare Phase:**  
The Proposer sends a request with a unique proposal number.  
Acceptors promise not to accept any proposal with a smaller number.

**Accept Phase:**  
If a majority agrees, the Proposer sends the actual value to be accepted.

### The Problem
Paxos is **extremely hard to understand** (even for senior engineers) and **difficult to implement correctly**.

There is no single “official” implementation, which caused companies (like Google with **Chubby**) to build their own customized versions.

---

## 2. Raft — “The Understandable Algorithm”
Raft was introduced in **2013** as an alternative to Paxos.  
Its main goal was **understandability and teachability**, without sacrificing performance.

### Philosophy
Raft relies on a **Strong Leader** model.

### How It Works
Raft divides consensus into **three sub-problems**:

#### Leader Election
If the current leader fails, the cluster starts an election and chooses a new leader that has the **most up-to-date log**.

#### Log Replication
The leader is the **only node** that receives client requests.  
It replicates log entries to followers and commits them **only after a quorum** acknowledges storage.

#### Safety
Raft guarantees that any elected leader **must contain all previously committed log entries**.

---

## Comparison

| Aspect | Paxos | Raft |
|------|------|------|
| Clarity | Extremely complex and non-intuitive | Designed to be easy to understand |
| Leadership | Can work without a permanent leader (Multi-Paxos) | Fully leader-based (simpler management) |
| Implementation | Very difficult; bugs are common | Easier to implement; mature libraries exist |
| Performance | Comparable; Paxos may outperform in very rare cases | Excellent for most production workloads |

---

## 3. Why These Algorithms Matter in MLOps & AI

### Kubernetes (etcd)
Kubernetes is the core platform of **MLOps**.  
Its state database (**etcd**) runs on **Raft**.  
Without it, the cluster would not know which containers are running or stopped.

### Model Metadata Stores
In end-to-end AI systems, you need a reliable store for **model metadata**.  
Distributed databases with strong guarantees (e.g., **CockroachDB**) use Raft to ensure model metadata is never lost.

### Service Discovery
In large systems, models often need to communicate with other services (e.g., Vector Databases).  
Consensus algorithms ensure all servers have **accurate and up-to-date service addresses**.

---

## Engineer’s Advice
If you are currently building an **end-to-end AI system**, focus on **Raft**.  
It is the algorithm you will encounter in most modern tools such as:
- Consul
- etcd
- Kafka (newer versions)

Keep **Paxos** as **general knowledge**, unless you plan to build a database engine from scratch.
