# ServiceHub - Home Service Request System

## 📌 Overview

**ServiceHub** is a microservice-based Home Service Request System. This repository/documentation covers the following core microservices:

| Microservice | Responsibility | Database |
|---|---|---|
| [User Service](#-user-service) | User registration, login, user management, roles, password handling | MySQL |
| [Provider Service](#-provider-service) | Service provider management, availability, provider service details | MySQL |
| [Request Service](#-request-service) | Creating, viewing, updating, and managing service requests | MongoDB |

All services are built with **Java 25** and **Spring Boot**, use **Spring Cloud Config** for centralized configuration, and register with **Eureka** for service discovery. External traffic is routed through a shared **API Gateway** (port `8080`).

---

## 👨‍🎓 Student Information

| Information | Details |
|---|---|
| Student Name | Yashoda Gunawardhana |
| Student ID | 241711077 |
| Project | ServiceHub |
| GCP Project ID | project-a6d8ea92-fb5d-4ed6-99d |

---

## 🏗️ Overall System Architecture

```
                       ServiceHub Frontend
                              |
                              v
                       API Gateway :8080
                              |
        +---------------------+---------------------+
        |                     |                     |
        v                     v                     v
  User Service :8081   Request Service :8082   Provider Service :8083
        |                     |                     |
        v                     v                     v
     MySQL                MongoDB                MySQL

        +------------------+------------------+
        |                                     |
        v                                     v
 Config Server :8888                  Eureka Server :8761
```

---

## 🔌 Service Information Summary

| Property | User Service | Request Service | Provider Service |
|---|---|---|---|
| Service Name | user-service | request-service | provider-service |
| Port | 8081 | 8082 | 8083 |
| Database | MySQL | MongoDB | MySQL |
| Database Type | Relational | Non-Relational | Relational |
| API Gateway | 8080 | 8080 | 8080 |
| Eureka Server | 8761 | 8761 | 8761 |
| Config Server | 8888 | 8888 | 8888 |

---

## 🔗 GitHub Repositories

- User Service: https://github.com/yashodha-gunawardana/user-service
- Request Service: https://github.com/yashodha-gunawardana/request-service
- Provider Service: https://github.com/yashodha-gunawardana/provider-service

Each service is included in the main ServiceHub project as a Git submodule:

```
ServiceHub/
└── backend/
    └── services/
        ├── user-service/
        ├── request-service/
        └── provider-service/
```

---

## 🚀 Getting Started (All Services)

### Prerequisites

- Java JDK 25
- MySQL (for User Service & Provider Service)
- MongoDB (for Request Service)
- Git

Before starting any business service, make sure these are running:

- **Config Server** (`:8888`)
- **Eureka Server** (`:8761`)

### General Run Commands

**Windows**
```bash
.\mvnw.cmd spring-boot:run
```

**Linux / macOS**
```bash
./mvnw spring-boot:run
```

### Build

```bash
.\mvnw.cmd clean package
```

### Run Tests

```bash
.\mvnw.cmd test
```

> ⚠️ Do not commit passwords or other sensitive information to GitHub.

---

## 👤 User Service

### Overview
Manages user-related functionalities: registration, login, user management, roles, password handling, and validation. Uses **MySQL**.

### Technology Stack
- Java 25, Spring Boot 4.1.0, Spring Cloud 2025.1.2
- Spring Data JPA, Spring Web MVC, Spring Validation
- Spring Security Crypto (secure password handling — passwords are never stored as plain text)
- Spring Cloud Config, Eureka Client
- MySQL, Maven, Lombok

### Architecture
```
Frontend → API Gateway :8080 → User Service :8081 → MySQL
                                       ↑
                        Config Server :8888 / Eureka Server :8761
```

### Database
Stores: user details, email, password, user role, account information.

```sql
CREATE DATABASE servicehub_user_db;
```

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/servicehub_user_db
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD
```

### Project Structure
```
user-service/
├── src/main/java/
├── src/main/resources/
├── src/test/
├── .gitignore
├── mvnw / mvnw.cmd
├── pom.xml
└── README.md
```

### Status
Java 25 ✅ | Spring Boot ✅ | MySQL ✅ | Spring Data JPA ✅ | Eureka Client ✅ | Config Client ✅ | Validation ✅ | Password Security ✅ | GitHub ✅ | GCP Deployment ⏳

Repo: https://github.com/yashodha-gunawardana/user-service

---

## 🧰 Provider Service

### Overview
Manages service providers: provider information, availability, service details, and supports service request assignments. Uses **MySQL**.

### Technology Stack
- Java 25, Spring Boot, Spring Cloud, Spring Data, Spring Web
- Spring Cloud Config, Eureka Client
- MySQL, Maven, Lombok

### Architecture
```
Frontend → API Gateway :8080 → Provider Service :8083 → MySQL
                                        ↑
                        Config Server :8888 / Eureka Server :8761
```

### Database
Manages service provider information via Spring Data over MySQL.

### Project Structure
```
provider-service/
├── src/main/java/
├── src/main/resources/
├── src/test/
├── .gitignore
├── mvnw / mvnw.cmd
├── pom.xml
└── README.md
```

### Status
Java 25 ✅ | Spring Boot ✅ | MySQL ✅ | Eureka Client ✅ | Config Client ✅ | GitHub ✅ | GCP Deployment ⏳

Repo: https://github.com/yashodha-gunawardana/provider-service

---

## 📋 Request Service

### Overview
Manages customer service requests: creating, viewing, updating, and tracking request status. Uses **MongoDB**.

### Technology Stack
- Java 25, Spring Boot, Spring Cloud, Spring Web
- Spring Data MongoDB
- Spring Cloud Config, Eureka Client
- MongoDB, Maven, Lombok

### Architecture
```
Frontend → API Gateway :8080 → Request Service :8082 → MongoDB
                                        ↑
                        Config Server :8888 / Eureka Server :8761
```

### Database
Stores: request details, customer information, service details, request status, request dates.

### Project Structure
```
request-service/
├── src/main/java/
├── src/main/resources/
├── src/test/
├── .gitignore
├── mvnw / mvnw.cmd
├── pom.xml
└── README.md
```

### Status
Java 25 ✅ | Spring Boot ✅ | MongoDB ✅ | Spring Data MongoDB ✅ | Eureka Client ✅ | Config Client ✅ | GitHub ✅ | GCP Deployment ⏳

Repo: https://github.com/yashodha-gunawardana/request-service

---

## 📌 Overall Project Status

| Component | Status |
|---|---|
| User Service | ✅ Implemented |
| Provider Service | ✅ Implemented |
| Request Service | ✅ Implemented |
| Config Server | ✅ Running (:8888) |
| Eureka Server | ✅ Running (:8761) |
| API Gateway | ✅ Running (:8080) |
| GCP Deployment | ⏳ Pending |
