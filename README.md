# DeepSeek - Microservices Architecture

## Team 
- Rouaa Mahmoudi (3IDL1)  
- Sarah Hosni (3IDL1)  
- Maha Houidi (3IDL1)

## Description
DeepSeek is a modular, scalable microservices platform designed for AI-driven search and analysis.  

### Architecture Overview
1. **Access Layer:** Web, Mobile, and external APIs → via a secure API Gateway with centralized authentication.  
2. **Core Services:** Users, Search, ML, Notifications, Billing → decoupled and autonomous microservices.  
3. **Support Services:** Logs, Configuration, Audit → for observability and security.  
4. **Infrastructure:** Databases, Message Broker (async), Kubernetes, Monitoring → scalability and resilience.

**Advantages:** Evolutive, secure, observable, highly available — ideal for large-scale AI and search applications.

## Critique
DeepSeek uses **deep learning models**, specifically a **Mixture-of-Experts (MoE) architecture**, rather than a traditional expert system.

**Reasoning:**  
- Traditional Expert Systems: Use explicitly programmed logical rules and a structured knowledge base.  
- DeepSeek: Uses deep learning where complex reasoning behavior develops naturally through reinforcement learning without explicit programming.  

**MoE Architecture:**  
- Splits an AI model into separate sub-networks (“experts”), each specializing in a subset of input data.  
- This reduces training resource usage dramatically while maintaining high performance.

## Proposed ML Service Improvements
To complement parallelism and distribution, the ML service can be decomposed:  
1. **Model Management Service:** Handles trained models, versions, and deployment (MLOps).  
2. **Inference Service:** Dedicated service for executing predictions in parallel.  
3. **Training Service:** Automated training and orchestration (Airflow/Kubeflow).  

**Rationale:**  
- A single ML service is too monolithic. Decomposition allows:
  - Better scalability  
  - Autonomous training pipelines  
  - Model updates without affecting inference  
  - Easier integration with MLOps tools
**Benefits:**  
- Independent scaling of inference and training.  
- Continuous model updates without downtime.  
- Easier integration with MLOps tools.

##Part2

## API Gateway Responsibilities
The API Gateway serves as the **single entry point** for clients:  
- Request validation and normalization  
- Security (WAF, OAuth2/JWT, mTLS)  
- Authentication and authorization (RBAC/ABAC)  
- Intelligent routing and service discovery  
- Load balancing  
- Rate limiting and throttling  
- Distributed caching  
- Data transformation (REST ↔ gRPC ↔ GraphQL)  
- Response aggregation  
- Monitoring, metrics, and distributed tracing

## UML Diagrams
The project includes **UML diagrams modeled in LaTeX**:
- High-level microservices architecture  
- Detailed internal architecture of the API Gateway

## Request Flow Example
1. Client sends a request (Web/Mobile)  
2. Request Handler receives and validates it  
3. Security Layer checks WAF rules, mTLS, OAuth2  
4. API Schema Validator ensures request compliance  
5. Authentication & Authorization verifies identity and permissions  
6. Routing Engine directs the request to the appropriate service  
7. Load Balancer selects the service instance  
8. Rate Limiter enforces quotas  
9. Caching Layer returns cached data if available  
10. Circuit Breaker & Retry Manager ensures reliability  
11. Data Transformation Layer converts protocols/formats  
12. Response Aggregator composes the final response  
13. Monitoring & Logging tracks metrics and traces  
14. Response is sent back to the client

# DeepSeek - Parallel Microservices Architecture
##Part 3 
## Team 
- Rouaa Mahmoudi (3IDL1)  

## Description
DeepSeek is a modular, scalable platform designed for AI-driven search and analysis. The system leverages **parallel microservices** and distributed components to maximize throughput and minimize latency for large-scale search requests.

---

## Parallel Architecture Overview
The parallel architecture of DeepSeek is designed to handle **massive numbers of client requests simultaneously**:

1. **Client Layer:** Web and Mobile clients interact through **CDN/Edge caches** to reduce latency.  
2. **API Layer:** A **clustered API Gateway** handles routing, authentication, load balancing, rate limiting, and data transformation.  
3. **Business Layer:**  
   - **API Orchestrator** distributes requests to the appropriate microservices.  
   - **User Service**, **RAG / Retrieval Service**, and **Inference Service** operate in parallel, handling requests independently.  
4. **Model Layer:**  
   - **Model Management & Serving Service** handles trained models and deployments.  
   - Communication is **asynchronous via a message broker (Kafka)** for high throughput and decoupled workflows.  
5. **Data Layer:** Sharded and replicated **databases**, **vector stores**, and **object storage** ensure fast access and parallel read/write operations.  
6. **Monitoring:** Centralized metrics, logging, and tracing ensure observability.

---

## Benefits of the Parallel Architecture
- **Optimal Resource Utilization:** Multiple inference workers process requests concurrently, maximizing throughput.  
- **High Scalability:** The system can scale horizontally by adding more workers and service instances.  
- **Fault Tolerance:** Failure of a single worker or service does not block the system.  
- **Reduced Latency:** Parallel processing allows requests to be handled simultaneously without queue congestion.  

---

## Proof of Optimality
The parallel architecture is conceptually optimal for high-load environments:  

- Let **N** be the number of worker instances and **R** the incoming requests.  
- Each worker can independently process a request → **throughput ≈ min(N, R)**.  
- Excess requests are queued asynchronously without blocking active workers.  
- Communication through **message brokers** ensures non-blocking coordination, making full use of available compute resources.  

Thus, for large-scale AI search operations, this architecture minimizes response time while maintaining reliability.

---

## Advantages of Moving to a Distributed System
Updating DeepSeek to a **distributed system** brings additional benefits:  
1. **No dependence on a single OS or clock** — critical for decentralized environments.  
2. **Horizontal scalability** to handle millions of concurrent requests.  
3. **Resilience and fault tolerance** — nodes can fail independently without affecting overall service.  
4. **Dynamic resource allocation** based on system load.  

---


## Request Flow Example
1. Client sends a request (Web/Mobile).  
2. Request goes through CDN → clustered API Gateway.  
3. API Gateway routes requests to **BFF or API Orchestrator**.  
4. Requests are dispatched in parallel to **User Service**, **RAG Service**, and **Inference Service**.  
5. Inference service calls **Model Management** asynchronously through the broker.  
6. Responses are aggregated, transformed, and returned to the client.  
7. Metrics and logs are collected for monitoring and tracing.

---



