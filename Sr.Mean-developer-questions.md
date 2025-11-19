# Sr Developer Tech Questions — Short & Clear Answers

---

## 1. Microservices

Microservices split an application into small, independent services where each service owns a single business capability.
Each service has its own database, deployment cycle, and scaling strategy.
They communicate using REST or message queues, improving scalability and fault isolation.

---

## 2. Monolith

A monolithic architecture keeps the entire application in one single codebase.
All modules run together and are deployed together.
Simple to start but becomes difficult to scale and maintain as the project grows.

---

## 3. Why Microservices?

* Independent scaling
* Independent deployments
* Fault isolation
* Tech flexibility
* Better team autonomy

---

## 4. Event Loop (Node.js)

The event loop manages and executes asynchronous operations.
It processes timers, promises, I/O callbacks, and ensures non-blocking behavior.
It allows Node to handle thousands of requests using a single thread.

---

## 5. Clustering

Clustering creates multiple Node.js worker processes across CPU cores.
A master process distributes requests among workers, improving throughput and availability.

---

## 6. Worker Threads

Worker threads run CPU-heavy tasks in parallel.
This keeps the main event loop free to handle incoming requests without blocking.

---

## 7. JWT (JSON Web Token)

A secure, stateless authentication token generated after login.
The client sends it with every request so the server can verify user identity.

---

## 8. JWT Parts

* **Header:** algorithm and token type
* **Payload:** user data & claims
* **Signature:** verification to prevent tampering

---

## 9. PM2

PM2 is a production-grade process manager for Node.js.
It supports auto restarts, log management, monitoring, and clustering.

---

## 10. Rate Limiting

Restricts number of API requests per user/IP in a time window.
Protects against DDoS, brute-force attacks, and abuse.

---

## 11. Redis Cache

Redis is an in-memory key-value store.
Used to cache frequently accessed data, reducing database load and improving API performance.

---

## 12. When to Use Express

* Lightweight and fast
* Flexible architecture
* Huge middleware ecosystem
* Ideal for most Node.js APIs

---

## 13. When to Use Hapi

* Enterprise-style structure
* Built-in validation via Joi
* Strong plugin system
* Security-focused design

---

## 14. Hapi Plugins

Reusable modules for routing, authentication, logging, and database logic.
Improve maintainability and team collaboration.

---

## 15. Smoke Test

Basic validation after deployment to ensure the system is functioning.

### Angular Smoke Test

* Component renders
* Buttons load
* Basic service/API calls work

### Node.js Smoke Test

* `/health` returns 200
* Server starts without errors
* Database connects successfully

---

## 16. Load Balancing

Distributes incoming traffic across multiple servers.
Ensures high availability, reliability, and prevents overload.

---

## 17. Vertical vs Horizontal Scaling

**Vertical Scaling:** Increase server power (CPU/RAM).
**Horizontal Scaling:** Add more servers.
Horizontal scaling is preferred for large systems.

---

## 18. ACID

* **Atomicity:** all or nothing
* **Consistency:** valid data state
* **Isolation:** transactions don’t conflict
* **Durability:** data persists even after crash

---

## 19. Middleware (Express & Hapi)

Middleware is a function that runs before your route handler. Used for logging, auth, validation, and modifying requests.

## 20. CORS

CORS controls which domains can access your API. Implemented using headers like `Access-Control-Allow-Origin`.

## 21. MongoDB Indexing

Indexes speed up queries by avoiding full collection scans. Common types: single-field, compound, text, TTL, unique.

## 22. Optimizing MongoDB Queries

Use projections, indexes, lean queries, pagination, and avoid `$regex` on large datasets.

## 23. Aggregation Pipeline

A step-by-step data processing pipeline using stages like `$match`, `$group`, `$lookup`, `$sort`, `$facet`.

## 24. NPM Scripts

Custom commands defined in `package.json` for building, testing, starting, and deploying.

## 25. Environment Variables

Used to store secrets and environment-specific values. Managed using `.env` and libraries like `dotenv` or Hapi `confidence`.

## 26. Error Handling (Global)

Central error handler to catch exceptions and return consistent responses. Prevents app crashes.

## 27. Logging (Prod Ready)

Use `Winston`, `Pino`, or Hapi `good` for structured logs. Helps in debugging and monitoring.

## 28. Async/Await vs Promises

Async/await gives cleaner syntax but works on top of promises. Promises manage multiple async operations.

## 29. Streams in Node.js

Handle large data in chunks (file upload, file read) without loading the entire file into memory.

## 30. File Upload Handling

Use `multer`, `busboy` or Hapi `payload` streams. Upload to S3/Cloud Storage.

## 31. Security Best Practices

* Escape input
* Rate limit
* Validate payloads (Joi)
* Use HTTPS
* Avoid storing passwords in plain text

## 32. WebSockets

Bi-directional communication for chat, notifications, real-time events.

## 33. RxJS Basics

Helps manage async streams. Common operators: `map`, `filter`, `switchMap`, `mergeMap`, `take`, `catchError`.

## 34. Angular Change Detection

New Angular uses signal-based reactivity. Older versions used Zone.js.

## 35. Angular Lazy Loading

Load modules only when needed to improve performance and reduce bundle size.

## 36. Angular Interceptors

Middleware for frontend HTTP requests. Used for JWT injection, error handling, and logging.

## 37. Angular Guards

Protect routes using `AuthGuard`, `RoleGuard`, or `CanDeactivate` guard.

## 38. CI/CD

Automates build, test, and deployment using GitHub Actions, GitLab, Jenkins, or Bitbucket Pipelines.

## 39. Unit Testing Concepts

Testing components, services, and API logic using Jasmine/Karma for Angular and Jest/Mocha for Node.

## 40. Deployment Checklist

* Env variables set
* Logs configured
* Security headers enabled
* CDN for static files
* Monitoring active
