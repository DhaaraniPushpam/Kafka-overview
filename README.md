# ⚡ Kafka Overview — A Practical Guide

A concise, practical guide to **Apache Kafka** — covering core concepts, setup, and real-world use cases. Built as a reference for developers learning distributed event streaming systems.

## 📌 What's Covered

### Core Concepts
- **Producer / Consumer / Broker** — the fundamental Kafka triangle
- **Topics & Partitions** — how Kafka organizes and parallelizes data
- **Consumer Groups** — load balancing message processing
- **Offsets** — how Kafka tracks message position (and why it matters)
- **Retention Policy** — Kafka as a durable log, not just a queue

### Architecture
- Kafka vs traditional message queues (RabbitMQ, ActiveMQ)
- When to use Kafka: event sourcing, log aggregation, real-time pipelines
- ZooKeeper vs KRaft mode (Kafka 3.x+)

### Practical Setup
- Local Kafka setup with Docker Compose
- Creating topics, producing messages, consuming messages
- Basic Python producer/consumer with `kafka-python`

## 🛠️ Tech Stack
- **Apache Kafka** — distributed event streaming platform
- **Docker / Docker Compose** — local Kafka cluster setup
- **Python (kafka-python)** — producer and consumer scripts
- **Zookeeper** — cluster coordination (legacy mode)

## 🚀 Quick Start with Docker
```bash
git clone https://github.com/DhaaraniPushpam/Kafka-overview
cd Kafka-overview
docker-compose up -d

# Create a topic
kafka-topics.sh --create --topic my-topic --bootstrap-server localhost:9092

# Produce a message
kafka-console-producer.sh --topic my-topic --bootstrap-server localhost:9092

# Consume messages
kafka-console-consumer.sh --topic my-topic --from-beginning --bootstrap-server localhost:9092
```

## 🧠 Key Takeaways
- Kafka is a **distributed commit log** — consumers pull at their own pace
- Partitions enable horizontal scaling — more partitions = more parallelism
- Consumer groups allow the same data to power multiple independent services
- Kafka retains messages even after consumption — enables replay

## 🔍 Real-World Use Cases
- Real-time fraud detection pipelines
- Log aggregation across microservices
- Event-driven architecture between services
- Data pipeline ingestion into data warehouses

---
*A reference guide for understanding distributed systems fundamentals — relevant to backend and data engineering roles.*
