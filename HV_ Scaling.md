## 1. Environment: Cloud vs In-house / On-Prem

Before starting, Kalb explains that your choice depends on where your servers are hosted:

- **Cloud:** Scaling is very easy; you do not buy physical hardware. Instead, virtualized resources are provisioned for you with a single click.
- **On-Prem:** Scaling is difficult because you are limited by room space, cabling, and the time required to purchase and install physical RAM or servers.

---

## 2. Vertical Scaling (Scaling Up)

This means making the **same machine** more powerful. Like a skyscraper, you add more floors on top of the same building.

**What do you upgrade?**  
CPU (processor), RAM (memory), Disk (storage capacity and speed), or Network (bandwidth).

**Advantage:**  
Very simple; no code changes or complex system redesign is required.

**Disadvantages:**
1. It has limits (there is always a maximum hardware capability).
2. **Single Point of Failure:** If this powerful machine fails, everything goes down.
3. **Diminishing Returns:** Doubling machine power often costs more than double the price (e.g., a 2× machine may cost 3× more).

---

## 3. Horizontal Scaling (Scaling Out)

This means adding **multiple smaller machines** that work together. Like building a city of small houses instead of one skyscraper.

**Advantages:**
1. **High Availability:** If one machine fails, others continue working.
2. Virtually unlimited (you can add hundreds or thousands of servers).
3. Cheaper in the long run (many commodity servers are cheaper than one supercomputer).

**Disadvantages:**  
More complex; it requires a **Load Balancer** and the application must be **Stateless**.

---

## 4. How to Choose? (Kalb’s Golden Rule for Performance and Cost)

Kalb proposes a smart step-by-step strategy:

**Step 1 – Balance:**  
Start with vertical scaling until resources are balanced. Do not pay for 100GB RAM while your CPU is running at 90% usage. Aim for balanced utilization (e.g., ~70% for each resource).

**Step 2 – Availability:**  
Move quickly to horizontal scaling with at least two machines to avoid total downtime if one server fails.

**Step 3 – Tipping Point:**  
Continue vertical scaling until upgrading a single machine becomes too expensive or unreasonable. At that point, start adding more machines horizontally.

---

## 5. Scaling by Service Type

- **API (Back-end):**  
  Very easy to scale horizontally because it is **Stateless** (user data is stored in an external database, not on the server itself).

- **Database:**  
  Very hard to scale horizontally because data must remain synchronized across nodes.

**Common Solution:**  
Vertical scaling (a very powerful database server) + **Read Replicas** (read-only copies to reduce load).

- **Front-end:**  
  In the cloud, front-end is usually hosted on **Serverless** services like AWS S3, which scale automatically.

---

## 6. The “Laptop” Example (Cost Explanation)

Kalb tells a story about a colleague who bought a laptop for $800 with 64GB storage.  
By paying an extra $200 (total $1000), she could get 1TB of storage — a massive performance improvement.  
However, upgrading from 1TB to 2TB might require paying an additional $500.

**Lesson:**  
At the beginning, small increases in cost produce huge performance gains (Vertical Scaling).  
After a certain point, improvements become very expensive, which is when horizontal scaling becomes the better option.

---

## Conclusion: When to Use What?

- Use **Vertical Scaling** early on because it is simple and provides significant performance gains for relatively low cost.
- Move to **Horizontal Scaling** when you need higher availability or when upgrading a single machine becomes prohibitively expensive.
