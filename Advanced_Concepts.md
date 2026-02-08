# Advanced Distributed Systems Concepts

## 1. Eventual Consistency
Imagine you are building a **Recommendation System** for an e-commerce platform.

**Idea:**  
When a user purchases a product, we update their interests.  
If the model on **Server A** knows this information immediately, and **Server B** learns it after 5 seconds, no disaster happens — the user just sees slightly outdated recommendations for a few seconds.

**Why do we use it?**  
To achieve maximum speed (**Low Latency**).  
The system does not force the user to wait until all servers worldwide are updated.

**Famous examples:**  
- Cassandra  
- Amazon S3  

---

## 2. Quorums (Majority Rule)
To ensure data correctness and avoid random or incorrect values, systems use **voting**.

If you have **5 servers (nodes)**, how do we know the data we read is correct?

**Formula:**  
`N / 2 + 1`  
With 5 servers → quorum = **3**

### Write Quorum (W)
When writing data, the system confirms success **only after at least 3 servers** acknowledge that the data has been stored.

### Read Quorum (R)
When reading data, the system queries 3 servers.  
If two return the same value and one returns stale data, the system trusts the **majority**.

**Benefit:**  
Protects the system from:
- A “lying” server  
- A server that was down and came back with outdated data  

---

## 3. Consensus Algorithms
These algorithms act as the **constitution** of a distributed system, defining how a leader is chosen.

### Raft (Most Common)
**How it works:**
- Servers hold **elections**
- The server that receives the majority of votes becomes the **Leader**
- The Leader handles all write requests and replicates them to the **Followers**

**If the Leader fails:**  
Other servers detect the failure immediately and start a new election within milliseconds (**self-healing**).

---

## Practical Applications

### Etcd
The backbone of **Kubernetes** (essential for MLOps).  
Uses **Raft** to store cluster state.

### Zookeeper
Used by **Kafka** to coordinate brokers.

---

## Why This Matters for You as an AI Engineer

### Distributed Training
When training large models across multiple GPUs or nodes, the system must synchronize **weights and gradients** — a direct application of **consensus**.

### Feature Stores
When using feature stores like **Feast**, you must understand whether features are:
- **Strongly Consistent**
- or **Eventually Consistent**

### High-Availability Production
Deploying models on **Kubernetes** requires understanding how nodes reach **consensus** on deployment state to avoid downtime.

---

## Interview Terminology (English)

- **Split Brain:**  
  A dangerous scenario where the cluster splits into two groups, and each believes it is the leader  
  (Solved using quorum).

- **Leader Election:**  
  The process of selecting the node responsible for coordination.

- **Log Replication:**  
  Copying commands from the leader to followers to keep data consistent.
