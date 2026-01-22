# 🎟️ Ticket Booking System – Microservices Architecture
<img width="1575" height="969" alt="image" src="https://github.com/user-attachments/assets/6a47492f-62a5-4392-9fff-78d244caa045" />

A **backend ticket booking platform** built using **Spring Boot and Java 21**, designed to demonstrate a **production-style microservices architecture**.  
This project focuses on **service separation, asynchronous messaging, resiliency, security, and API management**, rather than UI development.

---

## 📌 Project Overview

The system simulates a real-world ticket booking flow where users book tickets for events hosted at venues.  
It is implemented using **independent microservices** that communicate via **REST APIs** and **Apache Kafka**, with centralized security and routing handled by an **API Gateway**.

Key architectural goals:
- Loose coupling between services
- Scalability under high traffic
- Fault tolerance
- Secure access
- Clean API documentation

---

## 🏗️ Architecture

### Microservices
- **Inventory Service** – Manages venues, events, and ticket availability
- **Booking Service** – Entry point for ticket bookings
- **Order Service** – Processes bookings asynchronously
- **API Gateway** – Centralized routing, security, and resiliency

### Infrastructure Components
- **MySQL** – Persistent storage
- **Flyway** – Database schema migrations
- **Apache Kafka** – Event-driven communication
- **Keycloak** – OAuth2 authentication & authorization
- **Docker & Docker Compose** – Local infrastructure setup

---

## 🔁 Booking Flow

1. Client sends a booking request via **API Gateway**
2. API Gateway authenticates the request (OAuth2/JWT)
3. Booking Service:
   - Validates customer existence
   - Fetches inventory details from Inventory Service
   - Publishes a booking event to Kafka
4. Order Service:
   - Consumes booking event from Kafka
   - Saves order to database
   - Updates inventory synchronously
5. Client receives immediate booking confirmation

---

## 🧩 Services Breakdown

### Inventory Service
**Responsibilities**
- Manage venues and events
- Track remaining ticket capacity
- Update inventory after bookings

**Tech Stack**
- Spring Boot
- Spring Data JPA (Hibernate)
- MySQL
- Flyway
- Swagger / OpenAPI

---

### Booking Service
**Responsibilities**
- Accept booking requests
- Validate customers
- Check inventory availability
- Publish booking events to Kafka

**Highlights**
- Non-blocking, async event publishing
- REST-based synchronous validation

---

### Order Service
**Responsibilities**
- Consume booking events from Kafka
- Persist orders to database
- Update event inventory

**Highlights**
- Event-driven (no REST endpoints)
- Kafka consumer-based design

---

### API Gateway
**Responsibilities**
- Single entry point for all clients
- Route requests to backend services
- Enforce authentication and authorization
- Apply circuit breaker pattern
- Aggregate Swagger documentation

**Features**
- OAuth2 Resource Server
- Resilience4j Circuit Breaker
- Fallback routing
- Unified API documentation

---

## 🔐 Security

- OAuth2 implemented using **Keycloak**
- Client Credentials Grant
- JWT-based authentication
- API Gateway validates tokens before routing requests
- Backend services are not directly exposed

---

## ⚙️ Resiliency & Fault Tolerance

- **Circuit Breaker Pattern** using Resilience4j
- Prevents cascading failures
- Supports:
  - Failure thresholds
  - Timeout handling
  - Half-open recovery state
- Health monitoring via Spring Actuator

---

## 🗄️ Database Management

- Single MySQL instance
- Schema versioned using **Flyway**
- Migration-based approach ensures:
  - Consistent environments
  - Safe schema evolution
  - Easy onboarding for new developers

---

## 📄 API Documentation

- Swagger UI enabled for:
  - Inventory Service
  - Booking Service
- API Gateway aggregates all documentation into a **single UI**
- Documentation endpoints are publicly accessible
- APIs remain secured

---

## 🚀 Getting Started

### Prerequisites
- Java 21
- Maven
- Docker & Docker Compose
- MySQL Workbench (optional)
- Postman (for API testing)

### Run Locally
1. Start infrastructure:
   ```bash
   docker-compose up -d
   
### Run services in order:

- Inventory Service

- Booking Service

- Order Service

- API Gateway

### Access:

- API Gateway: http://localhost:8090

- Swagger Docs: http://localhost:8090/docs

- Kafka UI: http://localhost:884

- Keycloak: http://localhost:1891

###  This Project Demonstrates

- Real-world microservices architecture

- Event-driven systems with Kafka

- API Gateway patterns

- OAuth2 & JWT security

- Database migrations

- Resilience & fault tolerance

- Clean, documented APIs
