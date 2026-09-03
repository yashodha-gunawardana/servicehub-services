# ServiceHub – Business Microservices

ServiceHub is a **cloud-native home service request management system** developed as a microservice-based application for the **ITS 2130 – Enterprise Cloud Architecture** final project.

This repository contains the **business microservices** of the ServiceHub application:

| Microservice | Responsibility | Database |
|---|---|---|
| [User Service](#-user-service) | User registration, login, user management, roles, password handling | MySQL |
| [Request Service](#-request-service) | Creating, viewing, updating, and managing service requests | MongoDB |
| [Provider Service](#-provider-service) | Service provider management, availability, provider service details | MySQL |

All services are built with **Java 25** and **Spring Boot**, use **Spring Cloud Config** for centralized configuration, and register with **Eureka** for service discovery. External traffic is routed through the shared **API Gateway** (`:8080`).

---

## 👨‍🎓 Student Information

| Information | Details |
|---|---|
| Student Name | Yashoda Gunawardhana |
| Student ID | 241711077 |
| Project | ServiceHub |
| Component | services |
| GCP Project ID | `project-a6d8ea92-fb5d-4ed6-99d` |

---

## 🏗️ Overall System Architecture

```text
                       ServiceHub Frontend
                              │
                              ▼
                       API Gateway :8080
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
  User Service :8081   Request Service :8082   Provider Service :8083
        │                     │                     │
        ▼                     ▼                     ▼
     MySQL                MongoDB                MySQL

        ┌──────────────────┬──────────────────┐
        │                                     │
        ▼                                     ▼
 Config Server :8888                  Eureka Server :8761
```

### Request Flow

```text
Frontend
   │
   ▼
API Gateway
   │
   ▼
Eureka Service Discovery
   │
   ├───────────────► User Service ──► MySQL
   ├───────────────► Request Service ──► MongoDB
   └───────────────► Provider Service ──► MySQL
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

## 🗄️ Database Architecture

ServiceHub demonstrates both required database categories:

```text
User Service            Provider Service
     │                        │
     ▼                        ▼
   MySQL                    MySQL
(Relational)             (Relational)

Request Service
     │
     ▼
  MongoDB
(Non-Relational)
```

The use of both database types satisfies the mandatory database requirement of the Enterprise Cloud Architecture project.

---

## 🔗 GitHub Repositories

- User Service: https://github.com/yashodha-gunawardana/user-service
- Request Service: https://github.com/yashodha-gunawardana/request-service
- Provider Service: https://github.com/yashodha-gunawardana/provider-service

Each service is maintained as an independent GitHub repository and included in the main ServiceHub project as a Git submodule:

```text
ServiceHub/
└── backend/
    └── services/
        ├── user-service/       # Git Submodule
        ├── request-service/    # Git Submodule
        └── provider-service/   # Git Submodule
```

---

## 🛠️ Technology Stack

### Backend

- Java 25
- Spring Boot 4.1.0
- Spring Cloud 2025.1.2
- Spring Data (JPA / MongoDB)
- Spring Web MVC
- Spring Validation
- Spring Security Crypto (secure password handling for User Service)
- Spring Cloud Config, Eureka Client
- Maven, Lombok

### Databases

- **MySQL** – Relational database (User Service, Provider Service)
- **MongoDB** – Non-relational database (Request Service)

### Cloud Platform

- Google Cloud Platform (GCP)
- Compute Engine
- Managed Instance Groups
- Instance Templates
- Health Checks
- Load Balancing
- Cloud SQL
- Firestore
- Cloud Storage
- VPC Network
- Cloud NAT
- Cloud Router
- Firewall Rules
- Service Accounts

### Process Management

- PM2

---

## 🚀 Getting Started (All Services)

### Prerequisites

- Java JDK 25
- Maven
- Git
- MySQL (for User Service & Provider Service)
- MongoDB (for Request Service)
- PM2

Before starting any business service, make sure these are running:

- **Config Server** (`:8888`)
- **Eureka Server** (`:8761`)

### Clone the Repository

```bash
git clone <SERVICES_REPOSITORY_URL>
cd servicehub-services
```

### Initialize Git Submodules

```bash
git submodule update --init --recursive
```

### Update Submodules

```bash
git submodule update --remote --merge
```

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
./mvnw clean package -DskipTests
```

### Run Tests

```bash
./mvnw test
```

> ⚠️ Do not commit passwords or other sensitive information to GitHub.

---

## 👤 User Service

### Overview
Manages user-related functionality: registration, login, user management, roles, password handling, and validation. Uses **MySQL**.

### Technology Stack
- Java 25, Spring Boot 4.1.0, Spring Cloud 2025.1.2
- Spring Data JPA, Spring Web MVC, Spring Validation
- Spring Security Crypto (passwords are never stored as plain text)
- Spring Cloud Config, Eureka Client
- MySQL, Maven, Lombok

### Architecture
```text
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
```text
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

## 📋 Request Service

### Overview
Manages customer service requests: creating, viewing, updating, and tracking request status. Uses **MongoDB**.

### Technology Stack
- Java 25, Spring Boot, Spring Cloud, Spring Web
- Spring Data MongoDB
- Spring Cloud Config, Eureka Client
- MongoDB, Maven, Lombok

### Architecture
```text
Frontend → API Gateway :8080 → Request Service :8082 → MongoDB
                                        ↑
                        Config Server :8888 / Eureka Server :8761
```

### Database
Stores: request details, customer information, service details, request status, request dates.

### Project Structure
```text
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

## 🧰 Provider Service

### Overview
Manages service providers: provider information, availability, service details, and supports service request assignments. Uses **MySQL**.

### Technology Stack
- Java 25, Spring Boot, Spring Cloud, Spring Data, Spring Web
- Spring Cloud Config, Eureka Client
- MySQL, Maven, Lombok

### Architecture
```text
Frontend → API Gateway :8080 → Provider Service :8083 → MySQL
                                        ↑
                        Config Server :8888 / Eureka Server :8761
```

### Database
Manages service provider information via Spring Data over MySQL.

### Project Structure
```text
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

## 🔗 Service Registration

Each microservice registers itself with the **Eureka Service Registry**.

Expected registered services:

```text
USER-SERVICE
REQUEST-SERVICE
PROVIDER-SERVICE
```

The API Gateway uses Eureka service discovery to route requests to the appropriate microservice, so services communicate using service names instead of relying on fixed instance addresses.

---

## ☁️ GCP Deployment

The backend microservices are deployed to **Google Cloud Platform** using an **IaaS** deployment model.

The deployment architecture supports:

- Multiple VM instances
- Managed Instance Groups
- Automatic horizontal scaling
- Health checks
- High availability
- Multi-zone deployment
- Load balancing
- Automatic process recovery

The project requirements specify that backend microservices must support automatic horizontal scaling and must not run as single fixed instances.

### Cloud Storage

ServiceHub also demonstrates the use of **Google Cloud Storage**. At least one backend functionality uses a Cloud Storage bucket for file storage, with stored files accessible through the application API/frontend as required by the project specification.

---

## 🔄 PM2 Process Management

The microservices are managed using **PM2** on the deployed VMs. PM2 provides:

- Process management
- Automatic restart after failures
- Application logging
- Automatic startup after VM restart

This satisfies the mandatory process-management and automatic-restart requirement.

---

## 📁 Git Submodules

Initialize all microservice repositories:

```bash
git submodule update --init --recursive
```

Update the submodules:

```bash
git submodule update --remote --merge
```

Check submodule status:

```bash
git submodule status
```

---

## 📚 Project Requirements (ITS 2130)

The ServiceHub microservices follow the ITS 2130 – Enterprise Cloud Architecture requirements, including:

- Java 25
- Spring Boot
- Spring Cloud
- Spring Data
- Multiple microservices (min. 2, max. 5 — ServiceHub uses 3)
- Relational database (MySQL)
- Non-relational database (MongoDB)
- Config Server
- Eureka Service Registry
- API Gateway
- GCP cloud deployment
- High availability and auto scaling
- PM2 process management
- Git submodules / Polyrepo architecture

---

