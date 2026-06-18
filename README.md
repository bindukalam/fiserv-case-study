
Title: Real-Time Fraud Decisioning Pipeline for a Digital Payments Platform
Note at top: This is a case study describing system design and my contributions on a production project. Source code is proprietary to my employer and is not included here.

Problem:
A digital payments platform processing millions of card transactions daily needed faster fraud detection without increasing false-positive alerts that were burdening manual review teams. Slow query performance and synchronous bottlenecks were also limiting throughput during peak transaction periods.

My Role & Contribution:
I worked on the backend systems powering real-time card authorization, settlement, and fraud monitoring — owning both the event-streaming infrastructure and the AI-assisted decisioning layer added on top of it.

Architecture Approach:
Event-driven microservices in Java 17 and Spring Boot consumed transaction events through Apache Kafka, enabling real-time processing instead of batch cycles. Redis distributed caching sat in front of frequently accessed transaction data to reduce database load. For fraud decisioning specifically, OpenAI's API was integrated to generate human-readable explanations for flagged transactions, and a vector database stored embeddings of historical fraud patterns so new transactions could be compared against known fraud signatures using similarity search rather than static rule thresholds. Oracle and MongoDB queries were optimized with advanced indexing and partitioning to support the increased throughput. The full pipeline was containerized with Docker and deployed on AWS EKS, with CI/CD automated through Azure DevOps, Jenkins, and GitHub Actions.

Outcome:
API response latency dropped by approximately 40%. Database query p95 times improved by 35%. Mean time to detect production incidents dropped by 50% after adding Splunk-based observability and distributed tracing. Manual fraud review time decreased as AI-generated explanations reduced triage effort.

What I'd Explore Further:
Expanding the vector similarity approach to detect emerging fraud patterns in real time rather than relying solely on historical matches, and evaluating whether a managed vector database would outperform the current setup at higher transaction volumes.
