### 1. Core Concepts: Design vs. Architecture vs. System Design
* **Design Patterns:** Focus on code organization within a single project (e.g., how to structure files and classes).
* **Software Architecture:** Focus on how different high-level systems interact (e.g., databases, servers, and cloud integration).
* **System Design:** The process of solving specific technical challenges (e.g., scaling to millions of users) which results in a final architecture.

### 2. The MVC Design Pattern (Inside the App)
* **Router:** Maps the user's request (URL) to a specific function.
* **Controller:** The coordinator. It takes data from the Model and passes it to the View.
* **Model:** The only part responsible for interacting with the Database (CRUD operations).
* **View:** The presentation layer. It formats data into HTML/CSS for the user to see.

### 3. Monolith vs. Microservices
* **Monolith:** Everything (code, database, UI) is bundled into one single application and server. It’s simple but hard to scale.
* **Microservices:** The app is split into small, independent services. It's highly scalable but introduces complex communication challenges.
* **The Spectrum:** Most professional apps fall somewhere in the middle to avoid over-engineering.

### 4. Three-Tier Architecture
This approach separates the system into three physical or logical layers:
1.  **Presentation Tier (Front-end):** The user interface (React, HTML/CSS).
2.  **Application Tier (Back-end):** The logic and processing (Django, Node.js).
3.  **Data Tier (Database):** The storage layer (PostgreSQL, MySQL).

### 5. Practical Tech Stack & Hosting (AWS Example)
* **Front-end:** React (JavaScript) — Hosted on **AWS S3**.
* **Back-end:** Django (Python) — Hosted on **AWS EC2**.
* **Database:** PostgreSQL — Hosted on **AWS RDS**.

### 6. Why Architecture Matters: Scalability
Separating these layers allows you to scale them independently. If the traffic increases, you can add more Back-end servers or implement **Load Balancing** without needing to rewrite the entire system.
