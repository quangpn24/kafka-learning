# Kafka Connect
## Introduction
This repository provides a step-by-step guide to set up Kafka Connect. Kafka Connect is a framework to stream data between Apache Kafka and other systems in a reliable and scalable way.

## Architecture

## Installation

---
### Prerequisites
- Docker
- Docker Compose
---

### Step 1: Clone project
```bash 
git clone https://github.com/quangpn24/kafka-learning.git 
```
Then move to Kafka Connect directory 
```bash
cd kafka-learning/kafka-connect
```
### Step 2: Run docker-compose
```bash
docker-compose up -d
```
### Step 4: Setup connector
1. **Source connector**

 Use [JDBC source connector](https://docs.confluent.io/kafka-connectors/jdbc/current/source-connector/overview.html)
```bash
curl -X POST -H "Content-Type: application/json" --data @source/jdbc/mysql-todo-source.json http://localhost:8083/connectors
```
Or [Debezium source connector](https://docs.confluent.io/kafka-connectors/debezium-mysql-source/current/overview.html)
```bash
curl -X POST -H "Content-Type: application/json" --data @source/debezium/mysql-user-source.json http://localhost:8083/connectors
```
2. **Sink connector**

 Use [Elasticsearch sink connector](https://docs.confluent.io/kafka-connectors/elasticsearch/current/overview.html)
```bash
curl -X POST -H "Content-Type: application/json" --data @sink/elasticsearch/es-todo-sink.json http://localhost:8083/connectors
```

### Step 5: Setup password for account`kibana_system`
```bash
docker compose exec elastic sh
```
Then run
```bash
curl -X POST -u "elastic:${ELASTIC_PASSWORD}" -H "Content-Type: application/json" http://localhost:9200/_security/user/kibana_system/_password -d "{ \"password\": \"${KIBANA_PASSWORD}\" }"
```
After that, you can access Kibana at `http://localhost:5601` with username `your_username` (default: `elastic`) and password `your_password`.

---
And that's all you need to set up Kafka Connect. Good luck!