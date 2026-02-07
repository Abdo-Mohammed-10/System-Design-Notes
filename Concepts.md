**1. Distributed Systems**
**Concept:** Instead of running an application on a single computer, it is run across multiple machines that work together to present a single unified system to the user.
**Challenge:** How to make these machines communicate and coordinate as if they were one machine.

**2. Availability and the “Nines” System**
**Concept:** The ability of a system to remain operational and accessible 24/7.
**Measurement (Nines):** Availability is measured by the number of “9s” in the percentage:

* **90% (One Nine):** About 36.5 days of downtime per year (very poor).
* **99% (Two Nines):** About 3.65 days of downtime per year.
* **99.99% (Four Nines):** Less than one hour of downtime per year (a common target for most applications).
  **Rule:** Increasing the number of nines improves availability, but the cost and technical complexity increase exponentially.

**3. Reliability**
**Difference from Availability:** Availability means the service is reachable and responds to requests, while reliability means the service works correctly without data loss or incorrect results.
**Simple Example:** A friend who always answers the phone (high availability) but fails to help you move or complete the task properly (low reliability).

**4. Consistency**
**Definition:** All users see the same data at the same time.

* **Strong Consistency:** A data update is confirmed only after it has been applied to all servers (slower but more accurate, essential for banking systems).
* **Eventual Consistency:** One server is updated immediately, and the change propagates to others over time (faster, but users may see stale data for a short period, such as likes on Facebook).

**5. Scalability**
**Definition:** The system’s ability to handle increased workload or more users.

* **Over-provisioning:** Using hardware that is much more powerful than currently needed to avoid failures during peak load.
* **Vertical Scaling (Scaling Up):** Increasing resources (CPU, RAM) on a single server.
* **Horizontal Scaling (Scaling Out):** Adding more servers to work alongside existing ones.

**6. Elasticity**
**Concept:** The ability of a system to automatically increase resources during high load and reduce them when demand drops, optimizing cost (commonly provided by cloud platforms like AWS).

**7. Single Point of Failure (SPOF)**
**Concept:** Any component whose failure causes the entire system to stop (e.g., having only one database server).
**Solution:** **Redundancy**, by having backup components ready to take over immediately.

**8. Fault Tolerance**
**Concept:** Designing systems that continue operating even when some components fail, achieved by eliminating single points of failure and using redundancy.

**9. Database Replication**

* **Master / Write Node:** The primary server where data is written.
* **Slave / Read Replicas:** Read-only copies used to reduce load on the master.
* **Latency:** The time taken for a request from being sent to receiving a response.

**10. ACID Properties in Databases**
To ensure database reliability, four rules must be satisfied:

* **Atomicity:** A transaction is completed fully or not at all.
* **Consistency:** Data must always follow defined rules and constraints.
* **Isolation:** Concurrent transactions do not interfere with each other.
* **Durability:** Once data is committed, it remains saved even after power failure.

**11. Partitioning and Sharding**

* **Vertical Partitioning:** Splitting a table by columns.
* **Horizontal Partitioning:** Splitting a table by rows.
* **Sharding:** Distributing these partitions across multiple servers (nodes) to reduce load on a single machine.

**12. Caching**
**Concept:** Storing frequently accessed data in fast storage (such as memory) to reduce database load and improve performance.

**13. Serverless Technologies**
**Concept:** Serverless does not mean there are no servers; it means the cloud provider (e.g., AWS) manages scaling, availability, and infrastructure, and you pay only for what you use.

