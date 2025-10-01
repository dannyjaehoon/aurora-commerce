📦 Aurora Commerce

Aurora Commerce is a microservices-based e-commerce system built with Java Spring Boot.
It demonstrates key concepts for scalable backend systems: API Gateway, Kafka-based event-driven communication, caching, rate limiting, resilience patterns, and observability.

🚀 Features

Microservices Architecture with Spring Boot

API Gateway (Spring Cloud Gateway) with Redis Rate Limiting

Order Workflow using Kafka Saga pattern (Order → Inventory → Payment → Notification)

Caching Layer with Redis (product details, popular products)

Search Service powered by Elasticsearch

Recommendation Service (trending products via Kafka events)

Resilience4j for retries, timeouts, and circuit breakers

Observability Stack: Micrometer, Prometheus, Grafana, OpenTelemetry, Jaeger

Load Testing with k6 (p95 latency measurement)

🏗️ Architecture
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

📂 Services

api-gateway – Routing, authentication (JWT), rate limiting

product-service – Product CRUD, caching, event publishing

search-service – Elasticsearch integration for queries

order-service – Order management, Outbox pattern, Saga orchestration

inventory-service – Stock reservation and release

payment-service – Payment simulation (authorize/decline)

recommendation-service – Trending products from Kafka events

notification-service – Mock notifications (logs/email placeholder)

⚙️ Tech Stack

Java 17, Spring Boot 3.x

Spring Cloud Gateway, Resilience4j

Kafka (event-driven communication)

PostgreSQL (transactional data)

Redis (cache + rate limiter)

Elasticsearch (search service)

Prometheus + Grafana (metrics)

Jaeger + OpenTelemetry (distributed tracing)

k6 (load testing)

🧪 Example Flow

Client sends POST /orders via API Gateway

Order Service creates order + Outbox → publishes order.created

Inventory Service reserves stock → publishes inventory.reserved

Payment Service simulates payment → publishes payment.authorized or payment.declined

Order Service updates status → COMPLETED or FAILED

Notification Service consumes final event → sends confirmation (mocked)

📊 Observability & Performance

Dashboards: p50/p95/p99 latency, error rate, throughput

Rate limiting metrics (Redis Token Bucket)

Distributed traces across all services (Jaeger)

k6 load tests for search/product/order flows

▶️ Getting Started
Prerequisites

Docker & Docker Compose

Java 17

Gradle

Run Locally
# Start infrastructure (Kafka, Redis, PostgreSQL, Elasticsearch, Prometheus, Grafana, Jaeger)
docker-compose up -d

# Build all services
./gradlew clean build

# Run services (example)
cd product-service && ./gradlew bootRun

Access

API Gateway: http://localhost:8080

Grafana: http://localhost:3000

Jaeger UI: http://localhost:16686

Prometheus: http://localhost:9090

Kibana (for Elasticsearch): http://localhost:5601

📅 Roadmap (4 Weeks)

Week 1: Core setup, Product & Order services

Week 2: Inventory & Payment services, Saga workflow

Week 3: Rate limiting, caching, resilience, observability

Week 4: Search, recommendations, load testing, documentation

📖 Documentation

Detailed development notes, architectural decisions, and troubleshooting logs are maintained in Obsidian.
A summary and final results are published here in the README for recruiters and reviewers.

👤 Author

Jaehoon Lee – Backend Engineer (Java/Spring)

Portfolio: GitHub
 | LinkedIn (optional)
