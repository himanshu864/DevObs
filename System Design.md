---
tags:
  - "#devops"
references: 
date_created: 2025-07-27
date_modified: 2025-07-26
---
---

# CAP Theorem

**The Core Idea:** A distributed database can only guarantee **two** of the following three properties at the same time: **Consistency, Availability, or Partition Tolerance.**

### The Properties

* **C - Consistency:** Every read request receives the **most recent data**. All users see the same data at the same time.
* **A - Availability:** Every request to a working node gets a **response**. The system is always operational, even if some nodes are down. It doesn't guarantee the response is the most recent data.
* **P - Partition Tolerance:** The system continues to function even if there's a **communication failure** (a "partition") between nodes. The nodes themselves are still running but can't talk to each other.

### The Real-World Choice: AP vs. CP

For any large-scale system on the internet (like YouTube), **Partition Tolerance (P) is mandatory** because network failures are inevitable. Therefore, the real choice is between Consistency and Availability.

* **AP (Availability + Partition Tolerance):**
    * **What it is:** The system stays available but sacrifices strong consistency. Data will eventually become consistent across all nodes (**eventual consistency**).
    * **Example:** YouTube. It's better to let a user watch a video (Availability) even if the view count is slightly outdated (temporary inconsistency) than to show an error.
    * **Best for:** Systems where being always online is more critical than having perfectly up-to-date data (e.g., social media, content delivery).
* **CP (Consistency + Partition Tolerance):**
    * **What it is:** The system guarantees consistent data but may become unavailable during a network partition to avoid data conflicts.
    * **Example:** Banking Systems. It's better to temporarily block a transaction (Unavailable) than to allow a state where two people see different account balances (Inconsistent).
    * **Best for:** Systems where data accuracy is non-negotiable (e.g., financial transactions, e-commerce inventory).
* **CA (Consistency + Availability):**
    * **What it is:** A system that is consistent and available but cannot function if there is a network partition.
    * **Example:** A traditional single-server database. It's not a distributed system and thus isn't partition-tolerant.

---
## Micro-services Design Patterns

### Monolithic Architecture

A traditional approach where an entire application is built as a single, unified unit.

- **Characteristics:**
    - Everything is developed, deployed, and scaled as one piece.
    - Components are **tightly coupled**.
    - Communication between features happens in-memory, so **request latency is less**.
- **Drawbacks:**
    - **Difficult to debug** and maintain as the codebase grows.
    - A change in one part requires redeploying the entire application.
    - Scaling is inefficient; you must scale the whole application even if only one feature is under heavy load.

### Microservices Architecture

An architectural style that structures an application as a collection of small, autonomous services.

- **Advantages:**
    - **Services are independent and isolated**, allowing for separate development, deployment, and scaling.
    - **Easy to scale**: Scale only the services that need it.
    - **Easy to debug**: Faults are isolated to a single service.
    - **Easy to store**: Each service can use the database technology best suited to its needs.
- **Disadvantages / Challenges:**
    1. **Increased Latency**: Network calls between services can increase latency if the system is not decomposed properly (i.e., not **loosely coupled**).
    2. **Complex Monitoring**: **High monitoring** is required because services are dependent on each other. A change in one service's API can break others, so you can't update changes carelessly.
    3. **Distributed Transaction Management**: Transaction management is difficult. It's **hard to rollback** changes across multiple services since they have separate databases.
    4. **Implementing Joins**: Cross-database **JOINS are difficult** to implement.

### Key Design Patterns & Strategies

#### 1. Decomposition Patterns

The first step is breaking the monolith into microservices.

- **Decomposition by Business Capability:**
    - **Concept:** Services are organized around business functions. Requires good **knowledge of the business**.
    - **Example (Online Order Application):**
        - `Product Catalog Service`
        - `Order Management Service`
        - `Billing Service`
        - `User Account Service`
- **Decomposition by Subdomain:**
    - **Concept:** A more formal approach using **Domain-Driven Design (DDD)**. The application's problem space (Domain) is divided into logical sub-parts (**Subdomains**).
    - **Example:** The "Order Management" business capability could be a large microservice. It can be further broken down into subdomains like:
        - `Shopping Cart Service`
        - `Checkout Service`
        - `Shipping Service`
- **Strangler Fig Pattern (Migration Strategy):**
    - **Concept:** A method for **refactoring to microservices**. You **can't convert from monolithic to microservices at once**.
    - **Process:** A routing layer (like an API Gateway) is placed in front of the monolith. You gradually build new microservices and **route traffic slowly** from the old monolith to the new services, eventually "strangling" the monolith until the **microservices can take all the traffic**.

#### 2. Database Management Patterns

- **Database per Service (Recommended):**
    - **Concept:** Each microservice has its own **database for each individual service**.
    - **Pros:** **Easy to scale and modify** independently.
    - **Cons & Solutions:**
        - **Challenge:** Hard to maintain **ACID properties** across databases.
            - **Solution: SAGA Pattern.** A **sequence of local transactions**. Each service performs its transaction and publishes an **event**. If a step fails, compensating transactions are triggered by **failure events** to rollback the changes.
                - **Choreographed SAGA:** Services subscribe to each other's events to trigger the next step. Can lead to **cyclic dependencies**.
                - **Orchestrated SAGA:** A central **orchestrator** service tells each service what to do and manages the overall state, avoiding direct dependencies between services.
        - **Challenge:** Hard to implement **JOINs**.
            - **Solution: CQRS (Command Query Responsibility Segregation).**
                - **Segregation:** The pattern separates write operations (**Command**) from read operations (**Query**).
                - **How it works:** Write operations (**Create, Update, Delete**) go to the normal service databases. For complex queries, you maintain a separate, denormalized, read-only **duplicate joined database** that is optimized for querying. This read model is updated by subscribing to events from the write services.
- **Shared Database (Anti-Pattern):**
    - **Concept:** Multiple microservices share a single database schema.
    - **Pros:** **Easy ACID properties compliance** and **easy to implement JOIN queries**.
    - **Cons:**
        - **Hard to scale** storage or performance for a specific service.
        - **Hard to modify** the schema, as changes are **dependent** and can impact multiple services.
        - Breaks the principle of loose coupling.

#### 3. Communication & Integration Patterns

- **Communication:**
    - **Synchronous:** Services communicate directly via **API** calls (e.g., REST, gRPC). Simple but creates runtime coupling.
    - **Asynchronous:** Services communicate via **events** using a message broker (e.g., **Kafka**, RabbitMQ). Promotes loose coupling and resilience.
- **Integration (API Gateway):**
    - **Concept:** A single entry point for all clients. The **Gateway** handles requests by routing them to the appropriate backend service.
    - **Flow:** **User -> Frontend -> API Gateway -> Backend-to-Backend** communication.
    - **Responsibilities:** Can also handle authentication, rate limiting, and request transformation.

#### 4. Observability

- **Concept:** Because a system is distributed, you need robust **observation** and **monitoring**.
- **Pillars:**
    - **Logging:** Centralized logging to aggregate logs from all services.
    - **Metrics:** Collecting performance and health data from services.
    - **Tracing:** Tracking a single request as it flows through multiple services to identify bottlenecks and errors.

---
# How to Scale an application

