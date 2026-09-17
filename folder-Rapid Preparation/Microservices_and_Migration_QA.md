# Q&A: Microservices & Migration Strategies

## 1. What defines a Microservices Architecture?
**Answer:** It is an architectural style that structures an application as a collection of small, autonomous, and loosely coupled services. Each service models a specific business domain (Bounded Context), is independently deployable, and crucially, **owns its own database/datastore**. They communicate over a network via APIs or message brokers.

## 2. What is the hardest part of adopting Microservices?
**Answer:** **Data Consistency and Distributed Transactions.** In a monolith, you can use a single ACID SQL transaction to update an inventory count and process a payment simultaneously. In microservices, the inventory and payment databases are separate. If the payment succeeds but the network fails before updating inventory, you have inconsistent data. You must implement complex compensation logic (like the **Saga Pattern**) to handle these failures.

## 3. Compare the scaling capabilities of Monoliths vs. Microservices.
**Answer:** 
*   **Monoliths:** Require scaling the entire application (running more instances of the massive codebase), which wastes resources if only one small feature is under heavy load.
*   **Microservices:** Allow for **independent, granular scaling**. If the 'Checkout' service is experiencing a Black Friday traffic spike, you can spin up 100 extra instances of just the Checkout service, while leaving the 'User Profile' service at 2 instances.

## 4. What is a "Distributed Monolith" and why is it an anti-pattern?
**Answer:** A Distributed Monolith occurs when an application is split into separate microservices, but those services are still tightly coupled. For example, if Service A cannot function without making a synchronous network call to Service B, and Service B depends on Service C. If one goes down, they all fail. You have inherited all the network latency and complexity of microservices, but retained the tight coupling and fragility of a monolith.

## 5. What is a Modular Monolith and why choose it over Microservices?
**Answer:** A Modular Monolith is a single deployable application where the codebase is strictly segregated into independent modules that communicate only via defined interfaces, not by direct database access. It is chosen because it avoids the massive operational complexity and network latency of Microservices, while still enforcing the clean code boundaries needed for large teams to work without stepping on each other's toes.

## 6. What is the Strangler Fig Pattern?
**Answer:** It is a migration strategy for safely moving from a legacy Monolith to Microservices. Instead of a risky "big bang" rewrite, you incrementally build new features or replace old ones as independent microservices. You use an API Gateway to route specific traffic to the new microservice, while allowing the legacy monolith to handle everything else. Over time, the monolith shrinks as it is "strangled" by the new services.

## 7. What role does an API Gateway play in the Strangler Fig pattern?
**Answer:** The API Gateway acts as the traffic cop. It sits between the client and the backend systems. It allows the engineering team to transparently redirect traffic for specific endpoints (e.g., `/api/billing`) away from the Monolith and toward the newly created Billing Microservice, without the client applications ever knowing the backend architecture changed.

## 8. What does "Bounded Context" mean in the context of Microservices?
**Answer:** Originating from Domain-Driven Design (DDD), a Bounded Context is a logical boundary within a domain where a specific model and language apply. In microservices, a service should represent one Bounded Context (e.g., "Shipping"). The service should own everything related to Shipping (its logic, its data schema) and nothing else, ensuring high cohesion within the service and low coupling with other services.
