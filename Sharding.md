# Database Scaling Strategy (From Simple to Advanced)

## 1. Reduce Load Before “Scaling” (Pre-Scaling)
Kaleb advises **not to rush into database clustering**, because it is complex.  
There are critical steps to do **first**:

### Vertical Scaling
Upgrade the existing server to the maximum possible limits:
- Increase RAM
- Increase CPU

### Caching (Redis)
Use **Redis** to cache frequently requested data.  
This can reduce database queries by up to **80%**.

### Use Specialized Databases
Instead of putting everything in SQL, use purpose-built systems:

- **Elasticsearch**: for search
- **IndexedDB**: for storing simple data in the user’s browser (client-side)
- **Data Warehouse (OLAP)**: for large-scale analytics, isolated from the production OLTP database

---

## 2. Replication
Here, we create an **exact copy** of the data on another server.

### Goal
- High Availability
- Eliminate Single Point of Failure

### How It Works
A **Write-Ahead Log (WAL)** records every change on the primary database and streams it to replica servers.

### Important Note
Replication does **not reduce write load**.  
In fact, it **increases write cost**, because every write must be propagated to replicas.

---

## 3. Read Replicas
This is the most common way to scale **SQL databases**.

- **Master (Write Node):** only one server handles INSERT / UPDATE / DELETE
- **Slaves (Read Nodes):** multiple servers handle SELECT queries only

### Benefit
Most applications (e.g., Facebook) are **read-heavy**.  
So users who “browse” are distributed across replicas, while the master handles users who “post”.

### Challenge (Consistency)
Usually **Eventually Consistent**.  
You may publish a post and refresh immediately, but it might not appear yet on a read replica (seconds of delay).

---

## 4. Sharding
Here, data is **split**, not copied.

### Concept
If you have a table with 10 million users:
- First 5 million → Server 1
- Second 5 million → Server 2

### When to Use It
- When data no longer fits on a single disk
- When write volume becomes too high for a single server

### Shard Key
The key that determines where data goes:
- User ID
- Country (Geo-sharding)

---

## Replication vs Sharding

| Aspect | Replication | Sharding |
|------|------------|---------|
| Data Volume | Each server stores **all** data | Each server stores **a subset** |
| Primary Goal | Availability & read performance | Storage capacity & write scalability |
| Complexity | Simple (built-in in most systems) | Very complex (requires custom logic) |
| Example | Master-Slave (one writes, many read) | Horizontal partitioning (row-level split) |

---

## Kaleb’s Final Advice
If you are using **NoSQL databases** (e.g., MongoDB or Cassandra),  
you will find **Replication and Sharding much easier**, because they are **built into the database core**.

In contrast, **SQL databases** require significant manual effort and careful engineering.
