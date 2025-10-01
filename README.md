# 📦 Aurora Commerce

**Aurora Commerce** is a microservices-based e-commerce system built with **Java Spring Boot**.  
It demonstrates key concepts for scalable backend systems: API Gateway, Kafka-based event-driven communication, caching, rate limiting, resilience patterns, and observability.  

---

## 🚀 Features
- **Microservices Architecture** with Spring Boot  
- **API Gateway** (Spring Cloud Gateway) with Redis **Rate Limiting**  
- **Order Workflow** using **Kafka Saga pattern** (Order → Inventory → Payment → Notification)  
- **Caching Layer** with Redis (product details, popular products)  
- **Search Service** powered by Elasticsearch  
- **Recommendation Service** (trending products via Kafka events)  
- **Resilience4j** for retries, timeouts, and circuit breakers  
- **Observability Stack**: Micrometer, Prometheus, Grafana, OpenTelemetry, Jaeger  
- **Load Testing** with k6 (p95 latency measurement)  

---

## 📂 Services
- **api-gateway** – Routing, authentication (JWT), rate limiting  
- **product-service** – Product CRUD, caching, event publishing  
- **search-service** – Elasticsearch integration for queries  
- **order-service** – Order management, Outbox pattern, Saga orchestration  
- **inventory-service** – Stock reservation and release  
- **payment-service** – Payment simulation (authorize/decline)  
- **recommendation-service** – Trending products from Kafka events  
- **notification-service** – Mock notifications (logs/email placeholder)  

---

## ⚙️ Tech Stack
- **Java 17**, Spring Boot 3.x  
- **Spring Cloud Gateway**, Resilience4j  
- **Kafka** (event-driven communication)  
- **PostgreSQL** (transactional data)  
- **Redis** (cache + rate limiter)  
- **Elasticsearch** (search service)  
- **Prometheus + Grafana** (metrics)  
- **Jaeger + OpenTelemetry** (distributed tracing)  
- **k6** (load testing)

---

## 🏗️ Architecture
```mermaid
flowchart LR
    A[API Gateway] -->|REST| P[Product Service]
    A -->|REST| O[Order Service]
    A -->|REST| S[Search Service]
    A -->|REST| R[Recommendation Service]

    O -->|Kafka| I[Inventory Service]
    I -->|Kafka| Pay[Payment Service]
    Pay -->|Kafka| O
    O -->|Kafka| N[Notification Service]

    P -->|Events| S
    P -->|Cache| Redis[(Redis)]
    O -->|Outbox| Kafka[(Kafka)]
    S --> ES[(Elasticsearch)]



