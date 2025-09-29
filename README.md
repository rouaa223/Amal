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

## Proposed Improvements for ML Service
We propose **decomposing the monolithic ML service** into specialized sub-services:

1. **Model Management Service:** Manages trained models, versions, and deployment (MLOps).  
2. **Inference Service:** Handles prediction execution.  
3. **Training Service:** Performs automatic training and orchestration (via Airflow/Kubeflow).

**Rationale:**  
- A single ML service is too monolithic. Decomposition allows:
  - Better scalability  
  - Autonomous training pipelines  
  - Model updates without affecting inference  
  - Easier integration with MLOps tools

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

## Getting Started
1. Install LaTeX to compile UML diagrams  
2. Launch microservices using Docker/Kubernetes  
3. Configure API Gateway policies and service discovery  
4. Test endpoints using Postman or similar tools

## Observability
- Metrics: Prometheus  
- Tracing: OpenTelemetry  
- Logs: Centralized logging system
