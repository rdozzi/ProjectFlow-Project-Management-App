<h1> ProjectFlow (A multi-tenant project management application) </h1>

<h2 id="table-of-contents"> 0. Table of Contents </h2>
<ul style="padding: 0; list-style-type: none;">

<li><a href="#introduction">1. Introduction</a></li>
<li><a href="#architecture-overview">2. Architecture Overview</a></li>

  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#frontend">2.1 Frontend</a></li>
  <li><a href="#backend">2.2 Backend</a></li>
  <li><a href="#database">2.3 Database</a></li>

  </ul>
<li><a href="#application-features">3. Application Features</a></li>
  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#authentication-&-authorization">3.1 Frontend</a></li>
  <li><a href="#multi-tenant-organization-model">3.2 Multi-Tenant Organization Model</a></li>
  <li><a href="#entity-management">3.3 Entity Management</a></li>
  <li><a href="#multiple-task-views">3.4 Multiple Task Views</a></li>
  <li><a href="#file-attachments">3.5 File Attachments</a></li>
  <li><a href="#user-experience-and-ui">3.6 User Experience (UX) & UI</a></li>
  <li><a href="#system-foundations">3.7 System Foundations</a></li>

  </ul>

<li><a href="#testing-strategy">4. Testing Strategy</a></li>
  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#summary">4.1 Summary</a></li>
  <li><a href="#backend-testing">4.2 Backend Testing</a></li>
  
  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#coverage-for-deployed-routes">4.2.1 "Happy-path" Coverage for Deployed Routes</a></li>
  <li><a href="#selective-failure-mode-validation">4.2.2 Selective Failure-Mode Validation</a></li>
  <li><a href="#database-backed-integration-tests">4.2.3 Intentional exclusion of non-deployed routes</a></li>

  </ul>

  <li><a href="#fontend-testing">4.3 Frontend Testing</a></li>
  </li>
  </ul>

<li><a href="#environment-configuration">5. Environmental Configuration</a></li>
  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#environment-variables">5.1 Environmental Variables</a></li>
  <li><a href="#test-environment">5.2 Test Environment</a></li>
  <li><a href="#fronted-development">5.3 Frontend Environment</a></li>
  <li><a href="#redis">5.4 Redis</a></li>

  </ul>
<li><a href="#deployment">6. Deployment</a></li>
<li><a href="#known-limitations-and-future-work">7. Known Limitations & Future Work</a></li>
  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#environment-variables">7.1 Known Limitations</a></li>
  
  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#authentication-and-authorization-architecture">7.1.1 Authentication & Authorization Architecture</a></li>
  <li><a href="#testing-coverage">7.1.2 Testing Coverage</a></li>
  <li><a href="#scalability-and-performance">7.1.3 Scalability & Performance</a></li>
  <li><a href="#storage-and-infrastructure">7.1.4 Storage & Infrastructure</a></li>
  <li><a href="#authentication-enhancements">7.1.5 Authentication Enhancements</a></li>
  <li><a href="#testing-and-quality">7.1.6 Testing & Quality</a></li>
  <li><a href="#architecture-and-scalability">7.1.7 Architecture & Scalability</a></li>
  <li><a href="#deployment-and-devops">7.1.8 Deployment & DevOps</a></li>
  <li><a href="#product-features">7.1.9 Product Features</a></li>
  </ul>

  </ul>
  <li><a href="#reporting-and-contributing">8. Reporting and Contributing</a></li>
  <ul style="padding: 10; list-style-type: none;">

  <li><a href="#reporting-issues">8.1 Reporting Issues</a></li>
  <li><a href="#contributing">8.2 Contributing</a></li>
  </ul>
</ul>

<h2 id="introduction"> 1. Introduction</h2>

This is a Jira-like project management application MVP that I created as a part of a personal education project in my ongoing journey into fullstack web development and software engineering. The application is designed to manage tasks among teams of users representing tickets/issues in tabular, Kanban-like, and calendar views.

<h2 id="architecture-overview"> 2. Architecture Overview </h2>

<h3 id="frontend">Frontend</h3>
<ul style="padding-left: 1.25rem">
  <li>React - UI Framework
  <li>TypeScript - type-safe application logic
  <li>Ant Design - component library and design system
  <li>Vite - build tool and development server
</ul>

<h3 id="backend"> Backend </h3>
<ul style="padding-left: 1.25rem">
<li> Express.js - REST API Framework
<li> Node.js - Runtime environment
<li> Typescript - Application logic and contracts
<li> Prisma - ORM and migration tooling
</ul>

<h3 id="database"> Database </h3>
<ul style="padding-left: 1.25rem">
<li> PostgreSQL - Primary relational datastore
<li> Redis - Ephemeral data (counters, caching)
</ul>

<h2 id="application-features"> 3. Application Features </h2>

<h3 id="authentication-&-authorization"> Authentication & Authorization </h3>
<ul style="padding-left: 1.25rem">
<li> User authentication with token-based access control (JWT)
<li> Role awareness scoped to organizations and projects
<li> Tenant-level data isolation across all resources
</ul>

<h3 id="multi-tenant-organization-model"> Multi-Tenant Organization Model </h3>

<ul style="padding-left: 1.25rem">
<li> Organization-based hierarchy with user membership
<li> Separation of data between organizations
<li> Role-aware visibility of projects and tickets
</ul>

<h3 id="entity-management"> Entity Management </h3>
<ul style="padding-left: 1.25rem">
<li> Project, board, ticket, and comment hierarchy with full CRUD operations
<li> Board-level organization of tickets by status
<li> Assignments, due dates, priority, and status tracking for tickets
<li> Activity log generation and tracking for CRUD operations
</ul>

<h3 id="multiple-task-views"> Multiple Task Views </h3>
<ul style="padding-left: 1.25rem">
<li> List view with filtering capabilities
<li> Kanban board view for workflow management
<li> Calendar view listing tickets by due date
</ul>

<h3 id="file-attachments"> File Attachments </h3>
<ul style="padding-left: 1.25rem">
<li> Attachment upload and download capabilities for projects, boards, tickets, and comments
<li> Local and cloud (S3) storage layer
</ul>

<h3 id="user-experience-and-ui"> User Experience (UX) & UI </h3>
<ul style="padding-left: 1.25rem">
<li> UI/UX features based on Ant Design component library
<li> Light and Dark Theme support
</ul>

<h3 id="system-foundations"> System Foundations </h3>
<ul style="padding-left: 1.25rem">
<li> RESTful API architecture
<li> Centralized validation and error handling
<li> Environment-aware configuration for development and production
</ul>

<h2 id="testing-strategy"> 4. Testing Strategy </h2>

<h3 id="summary">Summary</h3>

The testing strategy implements a conscious balance of engineering rigor, pragmatic considerations and MVP delivery constraints that includes:

<ul style="padding-left: 1.25rem">
<li> Active backend logic that impacts data integrity, protection, segregation. and security within a multi-tenant database architecture
<li> Non-critical or deferred, "skipped," functionality is excluded from the initial test suite
<li> Frontend automation tests are postponed in favor of rapid iteration and manual validation
</ul>

<h3 id="backend-testing"> Backend Testing </h3>

The backend was tested primarily through integration tests designed to validate real application behavior across controllers, services, and the database.

Key Characteristics of the backend test approach include:

<h4 id="coverage-for-deployed-routes">"Happy-path" coverage for deployed routes </h4>

Core API endpoints including authentication, project/board/ticket/comment workflows, and attachment handling were tested for successful execution using realistic payloads and seeded data.

<h4 id="selective-failure-mode-validation">Selective failure-mode validation</h4>
Tests include representative failure scenarios such as invalid input, unauthorized access, and missing resources to ensure correct HTTP status codes and error handling behavior.

<h4 id="database-backed-integration-tests">Database-backed integration tests</h4>
Tests run against a dedicated test database, exercising Prisma queries, transactions, and relational constraints.

<h4 id="intentional-exclusion-of-non-deployed-routes">Intentional exclusion of non-deployed routes</h4>
Controller and routes that were deprecated, experimental, or explicitly deferred from the first deployment were skipped to keep test scope aligned with production functionality.

This approach ensures confidence in API correctness and data consistency without over-investing in test coverage for features not exposed in the MVP release.

<h3 id="fontend-testing"> Frontend Testing </h3>

No automated frontend tests were implemented for this MVP release.

This decision was intentional based on:

<ul style="padding-left: 1.25rem">
<li> The project is a portfolio MVP that prioritzes backend robustness and functionality.
<li> Time-constraint limits and the desire to reach a minimal deployment state (i.e. the MVP is "good enough" and "overdue" for deployment)

<li> Reliance on manual validation and qualitative smoke testing for UI flows, including:
</ul>

<ul style="padding-left: 2.50rem">
<li> Authentication and session handling
<li> Project, board, and ticket interactions
<li> File upload and download behavior
<li> State synchronization across views
</ul>

Frontend testing is intentionally deferred to post-deployment with future plans to introduce targeted component and integration tests.

<h2 id="environment-configuration"> 5. Environment Configuration </h2>

The environmental variables implemented within the application are separated between development, test, and production environments. Each environment uses its own database, cache, and storage configuration.

<h3 id="environment-variables">Environmental Variables (.env)</h3>

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

<h3 id="test-environment">Test Environment (.env.test)</h3>

The test environment uses overrides a subset of the developement environment variables to ensure deterministic and side-effect-free execution.

| **Variable** |        **Notes**        |
| :----------: | :---------------------: |
|   NODE_ENV   |   Always set to test    |
| DATABASE_URL | Points to test database |
|  JWT_SECRET  |  Non-production secret  |

<h3 id="fronted-development">Frontend Environment</h3>

The frontend does not require environment-specific configuration for this MVP.

<h3 id="redis"> Redis </h3>
Redis runs inside a local Docker container and is exposed on port 6379. 
The Node.js application connects via localhost using the Redis TCP protocol.

<h2 id="deployment"> 6. Deployment </h2>

The backend was deployed on Render using a production-specific TypeScript build configuration.

<h2 id="known-limitations-and-future-work"> 7. Known Limitations & Future Work </h2>

<h3 id="known-limitations"> Known Limitations </h3>

<h4 id="authentication-and-authorization-architecture"> Authentication & Authorization Architecture </h4>

<ul style="padding-left: 1.25rem">
<li> JWT-based auth<sup>1</sup>
<li> No refresh token rotation or server-side invaliation
<li> Route-level Role Based Access Control (RBAC); no fine-grained Authorization Control List (ACL)
</ul>

<sup>1</sup>For a browser-only MVP, a session-based authentication model would likely have reduced complexity around token invalidation and logout semantics. JWTs were selected to explore token-based patterns and for future API consumers.

<h4 id="testing-coverage"> Testing Coverage </h4>

<ul style="padding-left: 1.25rem">
<li> Backend integration tests only
<li> No frontend unit or E2E tests
</ul>

<h4 id="scalability-and-performance"> Scalability & Performance </h4>
<ul style="padding-left: 1.25rem">
<li> Tuned for small times; currently no load testing
<li> Limited Redis usage (no response caching)
</ul>

<h4 id="storage-and-infrastructure"> Storage & Infrastructure </h4>
<ul style="padding-left: 1.25rem">
<li>S3 tightly coupled; no storage abstraction
<li>No CDN for attachments
</ul>

<h4 id="ui-ux"> UI/UX </h4>
<ul style="padding-left: 1.25rem">
<li> Desktop-first layout (not optimized for tablet or mobile)
<li> Partial accessibility coverage (ARIA attributes, keyboard navigation)
</ul>

<h3 id="future-work">Future Work</h3>

<h4 id="authentication-enhancements"> Authentication Enhancements </h4>
<ul style="padding-left: 1.25rem">
<li> Refresh token rotation and session invalidation (possible authentication overall to hybrid token and session-based systems)
<li> OAuth / SSO providers
<li> More robust organization-level permission models
</ul>

<h4 id="testing-and-quality"> Testing & Quality </h4>
<ul style="padding-left: 1.25rem">
<li> Frontend unit testing
<li> E2E tesing for critical user flows
<li> Expanded backend test coverage
</ul>

<h4 id="architecture-and-scalability"> Architecture & Scalability </h4>
<ul style="padding-left: 1.25rem">
<li> Abstract storage providers behind a service interface
<li> Introduce query caching optimizations and query optimization
<li> Add rate-limit tuning and app-admin observability (metrics, structured logging)
</ul>

<h4 id="deployment-and-devops">Deployment & DevOps</h4>
<ul style="padding-left: 1.25rem">
<li> Containerized deployment with Docker
<li> CI/CD pipeline for automated testing and deployment
<li> Environment-specific configuration hardening
</ul>

<h4 id="product-features">Product Features</h4>
<ul style="padding-left: 1.25rem">
<li> Team communication: chats, polling, consistent asset update
<li> Notifications (email/in-app)
<li> Frontend toast notifications, improved frontend features
<li> Audit dashboards and organization usage analytics
</ul>

<h2 id="reporting-and-contributing"> 8. Reporting and Contributing </h2>

<h3 id="reporting-issues"> Reporting Issues </h3>
If you encounter a bug, unexpected behavior, or any other anomaly, please open an issue in the GitHub Issues tab.

Try to include the following:

<ul style="padding-left: 1.25rem">
<li> Steps to reproduce
<li> Expected vs actual behavior
<li> Relevant screenshots or logs if applicable
</ul>

This project is maintained on a best-effort basis.

<h3 id="contributing"> Contributing </h3>

Contributions are welcome for bug fixes, small enhancements, and documentation improvements.

For significant changes or new features, please open an issue first to discuss the proposal.

Basic workflow:

<ol style="padding-left: 1.25rem">
<li> Fork the repository
<li> Create a feature branch
<li> Commit clear and descriptive messages (My development workflow used the Conventional Commits extension)
<li> Submit a pull request with a brief explanation
</ol>

By contributing, you agree that your contributions will be licensed under the MIT License.
