# MySawit — Distributed Plantation Management Platform

MySawit is a distributed web platform for managing large-scale palm oil plantation operations using a modular microservice architecture.

This repository contains the `mysawit-auth` service (authentication and user management) as part of the larger MySawit system.

## Table of Contents
- [System Overview](#system-overview)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Core Modules](#core-modules)
- [Project Structure](#project-structure)
- [Service Architecture](#service-architecture)
- [Clean Code Principles](#clean-code-principles)
- [DevOps & Code Quality](#devops--code-quality)
- [Running the Project](#running-the-project)
- [Development Workflow](#development-workflow)
- [Future Improvements](#future-improvements)

---

## System Overview

MySawit coordinates workflows between plantation workers (buruh), supervisors (mandor), drivers (supir truk), and administrators. It tracks assignments, harvest reporting, logistics, and payroll while enforcing validation and traceability.

## Architecture

The platform follows a microservice architecture with a Database-per-Service pattern. Services communicate via REST APIs and asynchronous events where appropriate.

Key characteristics:
- Domain-driven service separation
- Independent deployment per service
- Loose coupling and clear responsibility boundaries
- Event-driven communication for asynchronous processes

Deployment and CI/CD:
- Fly.io for deployments
- GitHub Actions for CI/CD

## Tech Stack

- Backend: Spring Boot (Java)
- Authentication: JWT
- Database: PostgreSQL
- Object storage: Cloudflare R2
- Frontend (system-wide): Next.js
- CI/CD: GitHub Actions
- Testing: JUnit
- Coverage: JaCoCo
- Linting: Checkstyle (backend), ESLint (frontend)

## Core Modules

This service is part of a larger set of domain services such as:
- `mysawit-auth`
- `mysawit-plantation`
- `mysawit-harvest`
- `mysawit-delivery`
- `mysawit-payment`
- `mysawit-notification`

Within each service, common modules include:
- Authentication & User Management
- Plantation Management
- Harvest Management
- Delivery Management
- Payment Management
- Notification System

Each module owns its domain logic and database and exposes APIs for interaction.

## Project Structure

Typical layout for a service:

```
service-name/
├── Dockerfile
├── docker-compose.yml
├── build.gradle.kts
├── settings.gradle.kts
├── config/
│   └── checkstyle/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── (package)/
│   │   │       ├── controller/
│   │   │       ├── dto/
│   │   │       ├── entity/
│   │   │       ├── repository/
│   │   │       ├── service/
│   │   │       ├── security/
│   │   │       └── config/
│   │   └── resources/
│   │       ├── application.yml
│   │       └── static/
│   └── test/
└── gradle/
```

## Service Architecture

Layered responsibilities:

- Controller → handles HTTP endpoints and validation
- DTO → request/response objects
- Service → business logic and orchestration
- Repository → persistence (Spring Data JPA)
- Entity → JPA-mapped domain objects

## Clean Code Principles

The codebase follows SOLID principles, layered architecture, and DTO isolation to keep the API boundary clear and maintainable.

## DevOps & Code Quality

CI pipeline steps (GitHub Actions): build, lint, test, coverage.

Tools: Checkstyle, ESLint, JUnit, JaCoCo, CodeRabbit (code review automation).

## Running the Project

### Prerequisites

- Java 17+
- Docker (optional)
- Gradle (wrapper provided)
- PostgreSQL (or a running DB compatible with the configuration)

### Build

```bash
./gradlew build
```

### Run locally

```bash
./gradlew bootRun
```

### Run with Docker Compose

```bash
docker-compose up --build
```

## Development Workflow

Typical flow:
1. Create feature branch
2. Implement feature
3. Run tests and linting
4. Create a pull request
5. CI validation and code review
6. Merge and deploy
