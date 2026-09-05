# Q&A: Monolithic Architecture

## 1. What is a Monolithic Architecture?
**Answer:** It is an architectural style where an entire software application is designed, built, and deployed as a single, indivisible unit. 
*Example:* A Python Django application where the frontend templates, the user authentication logic, the e-commerce checkout logic, and the database connection logic are all in a single repository and run on a single web server process.

## 2. Why are Monoliths considered "high performance" compared to Microservices?
**Answer:** Inter-component communication is extremely fast because it relies on direct in-memory method calls. 
*Example:* If the `OrderService` needs to check if a user is valid, it simply calls `UserService.isValid(userId)`. This happens in a fraction of a millisecond in RAM. In a Microservice architecture, `OrderService` would have to make an HTTP/REST network call over the internet to a separate `UserService` server, which introduces network latency, serialization overhead (JSON parsing), and the risk of network failure.

## 3. How does scaling a Monolith differ from scaling Microservices?
**Answer:** 
*   **Monolith Scaling (All or Nothing):** You must scale the *entire* application. If only the "Reporting" module is receiving heavy traffic at the end of the month, you must deploy full copies of the entire application (including the idle UI and checkout modules) across multiple servers.
*   **Microservices Scaling (Granular):** You can scale components independently. You would just spin up 10 extra servers solely for the "Reporting Service" while leaving the rest of the application running on 1 server.

## 4. What is "Tight Coupling" and what is its impact on a Monolith?
**Answer:** Tight coupling occurs when different modules heavily depend on each other's internal code or share the same database tables. 
*Impact:* It increases the "blast radius" of bugs. 
*Example:* If a developer writes a bad SQL query in the "Image Upload" feature that locks the database or consumes 100% of the server's CPU, the entire application crashes. Users won't even be able to read plain text articles on the site because the single server process died. 

## 5. What are the deployment challenges of a massive Monolith?
**Answer:** As the codebase grows, deployments become rare, stressful events.
*Example:* In a massive monolith, running the automated test suite might take 2 hours. If a frontend developer wants to fix a simple typo on the homepage, they have to wait 2 hours for tests, and then coordinate with 50 other developers to deploy the massive payload. If anything goes wrong during the deploy (even a backend issue unrelated to the typo), the entire deploy must be rolled back, delaying the typo fix.

## 6. Should a startup begin with Microservices or a Monolith?
**Answer:** Generally, a startup should begin with a **Monolith**. Microservices introduce massive operational complexity (network latency, distributed tracing, complex CI/CD pipelines, container orchestration like Kubernetes). A monolith allows a startup to build their MVP (Minimum Viable Product) quickly to see if customers actually want the product. They can refactor into microservices later once they actually have the scaling problems that require them.

## 7. What is a "Modular Monolith"?
**Answer:** A Modular Monolith is a compromise. It is deployed as a single application, but the codebase is strictly organized into independent, isolated modules that are not allowed to directly access each other's databases or internal variables. 
*Example:* Shopify uses a massive Modular Monolith. They enforce strict rules so the `Billing` code folder cannot directly import code from the `Shipping` code folder; they must communicate through strictly defined internal APIs. This keeps the codebase clean and makes it very easy to break it apart into Microservices in the future.
