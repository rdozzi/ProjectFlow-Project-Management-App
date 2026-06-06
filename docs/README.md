# ProjectFlow (A multi-tenant project management application)

<!-- Start Table of Contents -->

## Table of Contents:

- [Introduction](#introduction)

- [Architecture Overview](#architecture-overview)
  - [Frontend](#frontend)
  - [Backend](#backend)
  - [Database](#database)

- [Application Features](#application-features)
  - [Authentication & Authorization](#authentication--authorization)
  - [Multi-Tenant Organization Model](#multi-tenant-organization-model)
  - [Entity Management](#entity-management)
  - [Multiple Task Views](#multiple-task-views)
  - [File Attachments](#file-attachments)
  - [User Experience & Interface](#user-experience-ux--ui)
  - [System Foundations](#system-foundations)

- [Testing Strategy](#testing-strategy)
  - [Summary](#summary)
  - [Backend Testing](#backend-testing)
    - [Happy-Path Coverage for Deployed Routes](#happy-path-coverage-for-deployed-routes)
    - [Selective Failure-Mode Validation](#selective-failure-mode-validation)
    - [Database-Backed Integration Tests](#database-backed-integration-tests)
    - [Intentional exclusion of non-deployed routes](#intentional-exclusion-of-non-deployed-routes)

  - [Frontend Testing](#frontend-testing)

- [Environmental Configuration](#environment-configuration)
  - [Environmental Variables](#environmental-variables-env)
  - [Test Environment](#test-environment-envtest)
  - [Frontend Environment](#frontend-environment)
  - [Redis](#redis)

- [Deployment](#deployment)

- [Known Limitations & Future Work](#known-limitations--future-work)
  - [Known Limitations](#known-limitations)
    - [Authentication & Authorization Architecture](#authentication--authorization-architecture)
    - [Testing Coverage](#testing-coverage)
    - [Scalability & Performance](#scalability--performance)
    - [Storage & Infrastructure](#storage--infrastructure)
  - [Future Work](#future-work)
    - [Authentication Enhancements](#authentication-enhancements)
    - [Testing & Quality](#testing--quality)
    - [Architecture & Scalability](#architecture--scalability)
    - [Deployment & DevOps](#deployment--devops)
    - [Product Features](#product-features)

- [Reporting and Contributing](#reporting-and-contributing)
  - [Reporting Issues](#reporting-issues)
  - [Contributing](#contributing)

<!-- End Table of Contents -->

## Introduction

This is a Jira-like project management application MVP that I created as a part of a personal education project in my ongoing journey into fullstack web development and software engineering. The application is designed to manage tasks among teams of users representing tickets/issues in tabular, Kanban-like, and calendar views.

## Architecture Overview

### Frontend

- React - UI Framework
- TypeScript - type-safe application logic
- Ant Design - component library and design system
- Vite - build tool and development server

### Backend

- Express.js - REST API Framework
- Node.js - Runtime environment
- Typescript - Application logic and contracts
- Prisma - ORM and migration tooling

### Database

- PostgreSQL - Primary relational datastore
- Redis - Ephemeral data (counters, caching)

## Application Features

### Authentication & Authorization

- User authentication with token-based access control (JWT)
- Role awareness scoped to organizations and projects
- Tenant-level data isolation across all resources

### Multi-Tenant Organization Model

- Organization-based hierarchy with user membership
- Separation of data between organizations
- Role-aware visibility of projects and tickets

### Entity Management

- Project, board, ticket, and comment hierarchy with full CRUD operations
- Board-level organization of tickets by status
- Assignments, due dates, priority, and status tracking for tickets
- Activity log generation and tracking for CRUD operations

### Multiple Task Views

- List view with filtering capabilities
- Kanban board view for workflow management
- Calendar view listing tickets by due date

### File Attachments

- Attachment upload and download capabilities for projects, boards, tickets, and comments
- Local and cloud (S3) storage layer

### User Experience & Interface

- UI/UX features based on Ant Design component library
- Light and Dark Theme support

### System Foundations

- RESTful API architecture
- Centralized validation and error handling
- Environment-aware configuration for development and production

## Testing Strategy

### Summary

The testing strategy implements a conscious balance of engineering rigor, pragmatic considerations and MVP delivery constraints that includes:

- Active backend logic that impacts data integrity, protection, segregation. and security within a multi-tenant database architecture
- Non-critical or deferred, "skipped," functionality is excluded from the initial test suite
- Frontend automation tests are postponed in favor of rapid iteration and manual validation

### Backend Testing

The backend was tested primarily through integration tests designed to validate real application behavior across controllers, services, and the database.

Key Characteristics of the backend test approach include:

#### Happy-Path coverage for deployed routes

Core API endpoints including authentication, project/board/ticket/comment workflows, and attachment handling were tested for successful execution using realistic payloads and seeded data.

#### Selective failure-mode validation

Tests include representative failure scenarios such as invalid input, unauthorized access, and missing resources to ensure correct HTTP status codes and error handling behavior.

#### Database-backed integration tests

Tests run against a dedicated test database, exercising Prisma queries, transactions, and relational constraints.

#### Intentional exclusion of non-deployed routes

Controller and routes that were deprecated, experimental, or explicitly deferred from the first deployment were skipped to keep test scope aligned with production functionality.

This approach ensures confidence in API correctness and data consistency without over-investing in test coverage for features not exposed in the MVP release.

### Frontend Testing

No automated frontend tests were implemented for this MVP release.

This decision was intentional based on:

- The project is a portfolio MVP that prioritzes backend robustness and functionality.
- Time-constraint limits and the desire to reach a minimal deployment state (i.e. the MVP is "good enough" and "overdue" for deployment)
- Reliance on manual validation and qualitative smoke testing for UI flows, including:
  - Authentication and session handling
  - Project, board, and ticket interactions
  - File upload and download behavior
  - State synchronization across views

Frontend testing is intentionally deferred to post-deployment with future plans to introduce targeted component and integration tests.

## Environment Configuration

The environmental variables implemented within the application are separated between development, test, and production environments. Each environment uses its own database, cache, and storage configuration.

### Environmental Variables (.env)

The backend requires the following environment variables to be defined:

|     **Variable**      |                                **Description**                                | **Required?** |
| :-------------------: | :---------------------------------------------------------------------------: | :-----------: |
|       NODE_ENV        |                              Runtime environment                              |      Yes      |
|         PORT          |                Port number _string_ for the Express.js server                 |      Yes      |
|     DATABASE_URL      |                          Postgres connection string                           |      Yes      |
|        DB_USER        |                              Postgres user name                               |      Yes      |
|        DB_HOST        |                             Postgres host string                              |      Yes      |
|        DB_NAME        |                             Postgres name string                              |      Yes      |
|      DB_PASSWORD      |                              DB password string                               |      Yes      |
|        DB_PORT        |                        DB port string (typically 5432)                        |      Yes      |
|     STORAGE_TYPE      | Either "LOCAL" or "CLOUD." "LOCAL" in development and "CLOUD" for production. |      Yes      |
|      JWT_SECRET       |                          JS web token secret string                           |      Yes      |
|   AWS_ACCESS_KEY_ID   |                      AWS access key (cloud storage only)                      |  Conditional  |
| AWS_SECRET_ACCESS_KEY |                      AWS secret key (cloud storage only)                      |  Conditional  |
|  AWS_DEFAULT_REGION   |                          Your region defined by AWS                           |  Conditional  |
|    AWS_BUCKET_NAME    |                          S3 bucket for file uploads                           |  Conditional  |

Attachments and general storage can either be stored in the local storage or in the AWS cloud. Hence, all AWS-related variabled are conditional.

### Test Environment (.env.test)

The test environment uses overrides a subset of the developement environment variables to ensure deterministic and side-effect-free execution.

| **Variable** |        **Notes**        |
| :----------: | :---------------------: |
|   NODE_ENV   |   Always set to test    |
| DATABASE_URL | Points to test database |
|  JWT_SECRET  |  Non-production secret  |

### Frontend Environment

The frontend does not require environment-specific configuration for this MVP.

### Redis

Redis runs inside a local Docker container and is exposed on port 6379.
The Node.js application connects via localhost using the Redis TCP protocol.

## Deployment

The backend was deployed on Render using a production-specific TypeScript build configuration.

## Known Limitations & Future Work

### Known Limitations

#### Authentication & Authorization Architecture

- JWT-based auth<sup>1</sup>
- No refresh token rotation or server-side invaliation
- Route-level Role Based Access Control (RBAC); no fine-grained Authorization Control List (ACL)

<sup>1</sup>For a browser-only MVP, a session-based authentication model would likely have reduced complexity around token invalidation and logout semantics. JWTs were selected to explore token-based patterns and for future API consumers.

#### Testing Coverage

- Backend integration tests only
- No frontend unit or E2E tests

#### Scalability & Performance

- Tuned for small teams; currently no load testing
- Limited Redis usage (no response caching)

#### Storage & Infrastructure

- S3 tightly coupled; no storage abstraction
  -No CDN for attachments

#### UI/UX

- Desktop-first layout (not optimized for tablet or mobile)
- Partial accessibility coverage (ARIA attributes, keyboard navigation)

### Future Work

#### Authentication Enhancements

- Refresh token rotation and session invalidation (possible authentication overall to hybrid token and session-based systems)
- OAuth / SSO providers
- More robust organization-level permission models

#### Testing & Quality

- Frontend unit testing
- E2E testing for critical user flows
- Expanded backend test coverage

#### Architecture & Scalability

- Abstract storage providers behind a service interface
- Introduce query caching optimizations and query optimization
- Add rate-limit tuning and app-admin observability (metrics, structured logging)

#### Deployment & DevOps

- Containerized deployment with Docker
- CI/CD pipeline for automated testing and deployment
- Environment-specific configuration hardening

#### Product Features

- Team communication: chats, polling, consistent asset update
- Notifications (email/in-app)
- Frontend toast notifications, improved frontend features
- Audit dashboards and organization usage analytics

## Reporting and Contributing

### Reporting Issues

If you encounter a bug, unexpected behavior, or any other anomaly, please open an issue in the GitHub Issues tab.

Try to include the following:

- Steps to reproduce
- Expected vs actual behavior
- Relevant screenshots or logs if applicable

This project is maintained on a best-effort basis.

### Contributing

Contributions are welcome for bug fixes, small enhancements, and documentation improvements.

For significant changes or new features, please open an issue first to discuss the proposal.

Basic workflow:

- Fork the repository
- Create a feature branch
- Commit clear and descriptive messages (My development workflow used the Conventional Commits extension)
- Submit a pull request with a brief explanation

By contributing, you agree that your contributions will be licensed under the MIT License.
