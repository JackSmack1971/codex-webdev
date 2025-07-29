# 🚀 Codex WebDev

> **Enterprise-Grade Web Development Template for 2025**  
> AI-Native • TypeScript-First • Production-Ready • DevSecOps Integrated

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20+-green.svg)](https://nodejs.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-1.28+-326CE5.svg)](https://kubernetes.io/)

## 📋 Table of Contents

- [Overview](#overview)
- [🎯 Key Features](#-key-features)
- [🏗️ Architecture](#️-architecture)
- [🛠️ Technology Stack](#️-technology-stack)
- [🚀 Quick Start](#-quick-start)
- [📁 Project Structure](#-project-structure)
- [🤖 AI-Guided Development](#-ai-guided-development)
- [💻 Development Guide](#-development-guide)
- [🔒 Security & DevOps](#-security--devops)
- [🧪 Testing Strategy](#-testing-strategy)
- [🚀 Deployment](#-deployment)
- [📚 Documentation](#-documentation)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

## Overview

**Codex WebDev** is a comprehensive, enterprise-grade web development template designed for 2025's modern development landscape. It combines cutting-edge technologies with AI-native development practices, providing a complete foundation for building scalable, secure, and maintainable web applications.

### 🌟 What Makes This Special?

- **🤖 AI-Native Development**: Unique AGENTS.md system guides AI coding assistants with context-aware instructions
- **🎯 2025-Ready Tech Stack**: Latest versions of React, Node.js, TypeScript, and modern tooling
- **🏗️ Enterprise Architecture**: Production-tested patterns with scalability and maintainability in mind
- **🔒 Security-First**: DevSecOps practices integrated from day one
- **📊 Multi-Database Strategy**: Support for SQL, NoSQL, and Vector databases for AI applications
- **🚀 Performance Optimized**: Core Web Vitals optimization and backend performance best practices

## 🎯 Key Features

### Development Experience
- ✅ **TypeScript Strict Mode** throughout the entire stack
- ✅ **Hot Reloading** with Vite for lightning-fast development
- ✅ **Comprehensive Linting** with ESLint and Prettier
- ✅ **Automated Testing** with Jest, React Testing Library, and Playwright
- ✅ **VS Code Integration** with recommended extensions and settings

### Architecture & Patterns
- ✅ **Layered Architecture** with clear separation of concerns
- ✅ **Repository Pattern** for data access abstraction
- ✅ **Service Layer** for business logic encapsulation
- ✅ **Atomic Design** for component organization
- ✅ **Event-Driven Architecture** with pub/sub patterns

### Production Readiness
- ✅ **Docker Containerization** with multi-stage builds
- ✅ **Kubernetes Orchestration** with helm charts
- ✅ **CI/CD Pipelines** with GitHub Actions
- ✅ **Monitoring & Observability** with OpenTelemetry
- ✅ **Security Scanning** integrated into pipelines

### Database & Storage
- ✅ **PostgreSQL** for relational data with advanced features
- ✅ **MongoDB** for document storage and flexible schemas
- ✅ **Redis** for caching and session management
- ✅ **Vector Databases** (Pinecone/Weaviate) for AI applications

## 🏗️ Architecture

### High-Level System Architecture

```mermaid
graph TB
    subgraph "Client Layer"
        Web[Web Browser]
        Mobile[Mobile App]
    end
    
    subgraph "Frontend Layer"
        React[React App<br/>TypeScript + Vite]
        Store[Redux Toolkit<br/>RTK Query]
        Components[Component Library<br/>Atomic Design]
    end
    
    subgraph "API Gateway"
        Gateway[Express.js Gateway<br/>Auth + Rate Limiting]
    end
    
    subgraph "Backend Services"
        Auth[Auth Service<br/>JWT + OAuth]
        User[User Service<br/>CRUD Operations]
        Business[Business Logic<br/>Domain Services]
    end
    
    subgraph "Data Layer"
        PostgreSQL[(PostgreSQL<br/>Primary Database)]
        MongoDB[(MongoDB<br/>Document Store)]
        Redis[(Redis<br/>Cache + Sessions)]
        Vector[(Vector DB<br/>AI/ML Data)]
    end
    
    subgraph "Infrastructure"
        Docker[Docker Containers]
        K8s[Kubernetes Cluster]
        Monitor[Monitoring<br/>Prometheus + Grafana]
    end
    
    Web --> React
    Mobile --> React
    React <--> Store
    React --> Components
    Store <--> Gateway
    Gateway --> Auth
    Gateway --> User
    Gateway --> Business
    
    Auth --> PostgreSQL
    Auth --> Redis
    User --> PostgreSQL
    User --> MongoDB
    Business --> PostgreSQL
    Business --> Vector
    
    Docker --> K8s
    K8s --> Monitor
```

### Backend Service Architecture

```mermaid
graph LR
    subgraph "Controllers Layer"
        UC[User Controller]
        AC[Auth Controller]
        BC[Business Controller]
    end
    
    subgraph "Middleware"
        Auth[Authentication]
        Valid[Validation]
        Rate[Rate Limiting]
        Log[Logging]
    end
    
    subgraph "Services Layer"
        US[User Service]
        AS[Auth Service]
        ES[Email Service]
        BS[Business Service]
    end
    
    subgraph "Repository Layer"
        UR[User Repository]
        AR[Auth Repository]
        BR[Business Repository]
    end
    
    subgraph "Database Layer"
        PG[(PostgreSQL)]
        MG[(MongoDB)]
        RD[(Redis)]
    end
    
    UC --> Auth
    AC --> Auth
    BC --> Auth
    
    Auth --> Valid
    Valid --> Rate
    Rate --> Log
    
    UC --> US
    AC --> AS
    BC --> BS
    
    US --> UR
    AS --> AR
    BS --> BR
    
    UR --> PG
    AR --> PG
    BR --> MG
    AS --> RD
```

### Frontend Component Hierarchy

```mermaid
graph TD
    subgraph "Application"
        App[App Component]
        Router[React Router]
        Store[Redux Store]
    end
    
    subgraph "Pages"
        Home[Home Page]
        Dashboard[Dashboard Page]
        Profile[Profile Page]
    end
    
    subgraph "Features"
        Auth[Auth Feature]
        UserMgmt[User Management]
        Settings[Settings Feature]
    end
    
    subgraph "Components (Atomic Design)"
        Organisms[Organisms<br/>Header, Sidebar, Forms]
        Molecules[Molecules<br/>SearchBox, Card, Modal]
        Atoms[Atoms<br/>Button, Input, Icon]
    end
    
    subgraph "Shared"
        Hooks[Custom Hooks]
        Utils[Utilities]
        Types[TypeScript Types]
        Services[API Services]
    end
    
    App --> Router
    App --> Store
    Router --> Home
    Router --> Dashboard
    Router --> Profile
    
    Home --> Auth
    Dashboard --> UserMgmt
    Profile --> Settings
    
    Auth --> Organisms
    UserMgmt --> Organisms
    Settings --> Organisms
    
    Organisms --> Molecules
    Molecules --> Atoms
    
    Auth --> Hooks
    UserMgmt --> Services
    Settings --> Utils
```

### Data Flow & Authentication

```mermaid
sequenceDiagram
    participant U as User
    participant F as Frontend
    participant G as API Gateway
    participant A as Auth Service
    participant S as Business Service
    participant D as Database
    participant R as Redis
    
    U->>F: Login Request
    F->>G: POST /auth/login
    G->>A: Validate Credentials
    A->>D: Query User Data
    D-->>A: User Details
    A->>R: Store Session
    A-->>G: JWT Tokens
    G-->>F: Auth Response
    F-->>U: Login Success
    
    Note over U,R: Subsequent API Calls
    
    U->>F: Business Action
    F->>G: API Request + JWT
    G->>G: Verify JWT
    G->>S: Process Request
    S->>D: Data Operation
    D-->>S: Result
    S-->>G: Response
    G-->>F: API Response
    F-->>U: Updated UI
```

### Database Entity Relationships

```mermaid
erDiagram
    USER {
        uuid id PK
        string email UK
        string password_hash
        string first_name
        string last_name
        enum role
        timestamp created_at
        timestamp updated_at
        timestamp deleted_at
    }
    
    SESSION {
        uuid id PK
        uuid user_id FK
        string token UK
        timestamp expires_at
        timestamp created_at
    }
    
    POST {
        uuid id PK
        string title
        text content
        boolean published
        uuid author_id FK
        timestamp created_at
        timestamp updated_at
    }
    
    USER_PREFERENCES {
        uuid id PK
        uuid user_id FK
        jsonb preferences
        timestamp created_at
        timestamp updated_at
    }
    
    USER ||--o{ SESSION : has
    USER ||--o{ POST : creates
    USER ||--|| USER_PREFERENCES : has
```

## 🛠️ Technology Stack

### Frontend Technologies

| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| React | 18+ | UI Framework | [React Docs](https://reactjs.org/) |
| TypeScript | 5.0+ | Type Safety | [TS Docs](https://www.typescriptlang.org/) |
| Vite | 5+ | Build Tool | [Vite Docs](https://vitejs.dev/) |
| Material UI | 5+ | UI Components | [MUI Docs](https://mui.com/) |
| Redux Toolkit | Latest | State Management | [RTK Docs](https://redux-toolkit.js.org/) |
| React Router | 6+ | Routing | [Router Docs](https://reactrouter.com/) |
| React Testing Library | Latest | Component Testing | [RTL Docs](https://testing-library.com/) |
| Playwright | Latest | E2E Testing | [Playwright Docs](https://playwright.dev/) |

### Backend Technologies

| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Node.js | 20+ | Runtime Environment | [Node.js Docs](https://nodejs.org/) |
| Express.js | 4.18+ | Web Framework | [Express Docs](https://expressjs.com/) |
| TypeScript | 5.0+ | Type Safety | [TS Docs](https://www.typescriptlang.org/) |
| Prisma | Latest | Database ORM | [Prisma Docs](https://www.prisma.io/) |
| JWT | Latest | Authentication | [JWT.io](https://jwt.io/) |
| Zod | Latest | Validation | [Zod Docs](https://zod.dev/) |
| Jest | Latest | Unit Testing | [Jest Docs](https://jestjs.io/) |
| Supertest | Latest | API Testing | [Supertest](https://github.com/visionmedia/supertest) |

### Database Technologies

| Database | Use Case | Features |
|----------|----------|----------|
| PostgreSQL 15+ | Primary relational data | ACID compliance, JSON support, full-text search |
| MongoDB 7+ | Document storage | Flexible schemas, aggregation pipelines |
| Redis 7+ | Caching & sessions | High performance, pub/sub, clustering |
| Pinecone/Weaviate | Vector storage | AI embeddings, semantic search |

### Infrastructure & DevOps

| Technology | Purpose | Configuration |
|------------|---------|---------------|
| Docker | Containerization | Multi-stage builds |
| Kubernetes | Orchestration | Helm charts included |
| GitHub Actions | CI/CD | Automated testing & deployment |
| Terraform | Infrastructure as Code | Multi-cloud support |
| Prometheus | Monitoring | Metrics collection |
| Grafana | Visualization | Custom dashboards |

## 🚀 Quick Start

### Prerequisites

Ensure you have the following installed:

- **Node.js** 20+ ([Download](https://nodejs.org/))
- **Docker** & Docker Compose ([Download](https://www.docker.com/))
- **Git** ([Download](https://git-scm.com/))
- **PostgreSQL** 15+ (or use Docker)
- **Redis** 7+ (or use Docker)

### 1. Clone & Setup

```bash
# Clone the repository
git clone https://github.com/your-org/codex-webdev.git
cd codex-webdev

# Install dependencies
npm install

# Copy environment files
cp frontend/.env.example frontend/.env
cp backend/.env.example backend/.env
```

### 2. Configure Environment

```bash
# Edit backend environment
nano backend/.env
```

<details>
<summary>📋 Backend Environment Variables</summary>

```env
NODE_ENV=development
PORT=8000

# Database
DATABASE_URL=postgresql://postgres:password@localhost:5432/app_db

# Redis
REDIS_URL=redis://localhost:6379

# JWT Keys (generate with openssl)
JWT_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----..."
JWT_PUBLIC_KEY="-----BEGIN PUBLIC KEY-----..."

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-password

# CORS
CORS_ORIGINS=http://localhost:3000
```

</details>

### 3. Start Development Environment

```bash
# Option 1: Docker Compose (Recommended)
docker-compose up -d

# Option 2: Local Development
npm run dev:services    # Start databases
npm run dev            # Start both frontend and backend
```

### 4. Initialize Database

```bash
# Run database migrations
npm run db:migrate

# Seed development data
npm run db:seed
```

### 5. Verify Installation

Navigate to:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8000
- **API Health**: http://localhost:8000/health

### 6. Run Tests

```bash
# Run all tests
npm test

# Run specific test suites
npm run test:unit        # Unit tests
npm run test:integration # Integration tests
npm run test:e2e        # End-to-end tests
```

## 📁 Project Structure

```
codex-webdev/
├── 📁 frontend/                 # React TypeScript application
│   ├── 📁 src/
│   │   ├── 📁 components/       # UI components (atomic design)
│   │   │   ├── 📁 atoms/        # Basic elements (Button, Input)
│   │   │   ├── 📁 molecules/    # Composed components (SearchBox)
│   │   │   └── 📁 organisms/    # Complex components (Header, Form)
│   │   ├── 📁 features/         # Feature-based organization
│   │   │   ├── 📁 auth/         # Authentication feature
│   │   │   ├── 📁 dashboard/    # Dashboard feature
│   │   │   └── 📁 profile/      # User profile feature
│   │   ├── 📁 hooks/           # Custom React hooks
│   │   ├── 📁 pages/           # Route components
│   │   ├── 📁 services/        # API integration
│   │   ├── 📁 store/           # Redux store & slices
│   │   ├── 📁 types/           # TypeScript definitions
│   │   ├── 📁 utils/           # Utility functions
│   │   └── 📁 assets/          # Static assets
│   ├── 📁 tests/               # Frontend tests
│   ├── 📄 vite.config.ts       # Vite configuration
│   ├── 📄 tsconfig.json        # TypeScript config
│   └── 📄 AGENTS.md            # Frontend AI guidance
│
├── 📁 backend/                  # Node.js Express API
│   ├── 📁 src/
│   │   ├── 📁 controllers/      # Route handlers
│   │   ├── 📁 services/         # Business logic
│   │   ├── 📁 repositories/     # Data access layer
│   │   ├── 📁 models/           # Data models
│   │   ├── 📁 middleware/       # Express middleware
│   │   ├── 📁 routes/           # API route definitions
│   │   ├── 📁 config/           # Configuration management
│   │   ├── 📁 types/            # TypeScript definitions
│   │   ├── 📁 utils/            # Utility functions
│   │   ├── 📄 app.ts            # Express app setup
│   │   └── 📄 server.ts         # Server initialization
│   ├── 📁 tests/               # Backend tests
│   ├── 📁 migrations/          # Database migrations
│   ├── 📄 Dockerfile           # Container definition
│   ├── 📄 tsconfig.json        # TypeScript config
│   └── 📄 AGENTS.md            # Backend AI guidance
│
├── 📁 database/                 # Database configurations
│   └── 📄 AGENTS.md            # Database AI guidance
│
├── 📁 infrastructure/           # DevOps configurations
│   ├── 📁 devops/
│   │   ├── 📁 k8s/             # Kubernetes manifests
│   │   ├── 📁 terraform/       # Infrastructure as Code
│   │   ├── 📁 monitoring/      # Observability configs
│   │   └── 📄 AGENTS.md        # DevOps AI guidance
│   └── 📁 docker/              # Docker configurations
│
├── 📁 docs/                     # Documentation
│   ├── 📄 api.md               # API documentation
│   ├── 📄 architecture.md      # Architecture decisions
│   └── 📄 deployment.md        # Deployment guide
│
├── 📁 scripts/                  # Build & deployment scripts
│   ├── 📄 setup.sh             # Initial setup
│   ├── 📄 deploy.sh            # Deployment script
│   └── 📄 test.sh              # Testing script
│
├── 📁 shared/                   # Shared types & utilities
│   ├── 📄 types.ts             # Common TypeScript types
│   └── 📄 constants.ts         # Shared constants
│
├── 📄 .codex/AGENTS.md         # Global AI guidance
├── 📄 AGENTS.md                # Project-level AI guidance
├──

### Benefits of the AGENTS.md System

- **🎯 Consistent Code Quality**: AI assistants follow your established patterns
- **⚡ Faster Development**: Reduced context switching and explanation overhead
- **📚 Knowledge Transfer**: New team members can understand conventions quickly
- **🔄 Iterative Improvement**: Guidelines evolve with your project
- **🤝 Team Alignment**: Shared understanding of best practices

## 💻 Development Guide

### Development Workflow

```mermaid
flowchart LR
    A[📝 Plan Feature] --> B[🌿 Create Branch]
    B --> C[🤖 AI-Guided Coding]
    C --> D[🧪 Write Tests]
    D --> E[✅ Run Quality Checks]
    E --> F[📋 Create PR]
    F --> G[🔍 Code Review]
    G --> H[🚀 Deploy]
    
    subgraph "Quality Gates"
        E1[Linting]
        E2[Type Check]
        E3[Unit Tests]
        E4[Integration Tests]
        E5[Security Scan]
    end
    
    E --> E1
    E --> E2
    E --> E3
    E --> E4
    E --> E5
```

### Available Scripts

#### Root Level Commands
```bash
# Development
npm run dev                 # Start both frontend and backend
npm run dev:frontend        # Start frontend only
npm run dev:backend         # Start backend only
npm run dev:services        # Start databases (Docker)

# Testing
npm test                    # Run all tests
npm run test:unit           # Unit tests only
npm run test:integration    # Integration tests only
npm run test:e2e           # End-to-end tests
npm run test:coverage      # Generate coverage report

# Quality Assurance
npm run lint               # Run ESLint
npm run lint:fix           # Fix linting issues
npm run type-check         # TypeScript type checking
npm run format             # Format code with Prettier

# Database
npm run db:migrate         # Run migrations
npm run db:seed           # Seed development data
npm run db:reset          # Reset database
npm run db:generate       # Generate Prisma client

# Build & Deploy
npm run build             # Build for production
npm run build:frontend    # Build frontend only
npm run build:backend     # Build backend only
npm run docker:build      # Build Docker images
npm run docker:run        # Run in Docker
```

### Code Quality Standards

#### TypeScript Configuration
```json
{
  "compilerOptions": {
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  }
}
```

#### ESLint Rules
- **Airbnb TypeScript** configuration
- **React Hooks** rules
- **Import ordering** enforcement
- **Accessibility** rules (jsx-a11y)

#### Prettier Configuration
- **2 spaces** indentation
- **Single quotes** for strings
- **Trailing commas** always
- **100 character** line length

### Git Workflow

#### Branch Naming Convention
```
feature/auth-system
bugfix/login-validation
hotfix/security-patch
refactor/user-service
docs/api-documentation
```

#### Commit Message Format
```
type(scope): description

feat(auth): add JWT refresh token mechanism
fix(user): resolve email validation issue
docs(readme): update installation instructions
test(auth): add integration tests for login
refactor(db): optimize user queries
```

### Environment Configuration

#### Development Environment
```bash
# Frontend (localhost:3000)
VITE_API_BASE_URL=http://localhost:8000
VITE_APP_NAME=Codex WebDev
VITE_ENVIRONMENT=development

# Backend (localhost:8000)
NODE_ENV=development
PORT=8000
DATABASE_URL=postgresql://postgres:password@localhost:5432/app_dev
REDIS_URL=redis://localhost:6379
LOG_LEVEL=debug
```

#### Production Environment
```bash
# Security considerations
NODE_ENV=production
JWT_PRIVATE_KEY=<secure-key>
DATABASE_URL=<production-db-url>
REDIS_URL=<production-redis-url>
LOG_LEVEL=info
```

## 🔒 Security & DevOps

### Security Implementation

#### Authentication & Authorization Flow

```mermaid
sequenceDiagram
    participant C as Client
    participant G as API Gateway
    participant A as Auth Service
    participant R as Redis
    participant D as Database
    
    Note over C,D: Login Process
    C->>G: POST /auth/login
    G->>A: Validate credentials
    A->>D: Check user exists
    D-->>A: User data
    A->>A: Verify password hash
    A->>R: Store session
    A-->>G: JWT tokens (access + refresh)
    G-->>C: Auth response
    
    Note over C,D: Protected Request
    C->>G: API request + JWT
    G->>G: Verify JWT signature
    G->>R: Check session validity
    R-->>G: Session confirmed
    G->>A: Authorize action
    A-->>G: Permission granted
    G-->>C: Protected resource
    
    Note over C,D: Token Refresh
    C->>G: POST /auth/refresh
    G->>A: Validate refresh token
    A->>R: Check refresh token
    R-->>A: Token valid
    A->>A: Generate new access token
    A-->>G: New JWT tokens
    G-->>C: Updated tokens
```

#### Security Features

| Feature | Implementation | Configuration |
|---------|---------------|---------------|
| **Authentication** | JWT with RS256 | 15min access, 7day refresh |
| **Authorization** | Role-based access control | Admin, User, Moderator roles |
| **Password Security** | bcrypt with 12 rounds | Enforced complexity rules |
| **Rate Limiting** | Express rate limit + Redis | 100 req/15min general, 5 req/15min auth |
| **CORS** | Configurable origins | Environment-specific |
| **Headers Security** | Helmet.js middleware | CSP, HSTS, X-Frame-Options |
| **Input Validation** | Zod schemas | Runtime type checking |
| **SQL Injection** | Parameterized queries | Prisma ORM protection |

### DevOps Pipeline

#### CI/CD Workflow

```mermaid
graph LR
    subgraph "Continuous Integration"
        A[🔍 Code Scan] --> B[🧪 Unit Tests]
        B --> C[🔒 Security Scan]
        C --> D[🏗️ Build Images]
        D --> E[📊 Integration Tests]
    end
    
    subgraph "Continuous Deployment"
        E --> F[🚀 Deploy Staging]
        F --> G[✅ E2E Tests]
        G --> H[🎯 Deploy Production]
        H --> I[📈 Monitor]
    end
    
    subgraph "Quality Gates"
        Q1[Lint & Format]
        Q2[Type Check]
        Q3[Test Coverage > 80%]
        Q4[Security Score > 8/10]
        Q5[Performance Budget]
    end
    
    A --> Q1
    B --> Q2
    B --> Q3
    C --> Q4
    G --> Q5
```

#### Monitoring & Observability

```mermaid
graph TB
    subgraph "Application"
        App[Web Application]
        API[API Server]
        DB[(Database)]
    end
    
    subgraph "Metrics Collection"
        Prom[Prometheus]
        OTel[OpenTelemetry]
        Logs[Centralized Logging]
    end
    
    subgraph "Visualization"
        Graf[Grafana Dashboards]
        Alert[Alert Manager]
        Jaeger[Distributed Tracing]
    end
    
    subgraph "External Services"
        Slack[Slack Notifications]
        PD[PagerDuty]
        Email[Email Alerts]
    end
    
    App --> OTel
    API --> OTel
    DB --> Prom
    
    OTel --> Prom
    OTel --> Logs
    OTel --> Jaeger
    
    Prom --> Graf
    Prom --> Alert
    
    Alert --> Slack
    Alert --> PD
    Alert --> Email
```

### Infrastructure as Code

#### Kubernetes Deployment

<details>
<summary>📋 Sample Kubernetes Manifests</summary>

```yaml
# k8s/namespace.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: codex-webdev
  labels:
    name: codex-webdev
    environment: production

---
# k8s/deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-deployment
  namespace: codex-webdev
spec:
  replicas: 3
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
      - name: backend
        image: codex-webdev/backend:latest
        ports:
        - containerPort: 8000
        env:
        - name: NODE_ENV
          value: "production"
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: app-secrets
              key: database-url
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
```

</details>

#### Terraform Infrastructure

<details>
<summary>🏗️ Infrastructure Components</summary>

```hcl
# infrastructure/terraform/main.tf
module "vpc" {
  source = "./modules/vpc"
  
  cidr_block = "10.0.0.0/16"
  environment = var.environment
  project_name = "codex-webdev"
}

module "eks_cluster" {
  source = "./modules/eks"
  
  cluster_name = "codex-webdev-${var.environment}"
  vpc_id = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnet_ids
  node_instance_types = ["t3.medium"]
  desired_nodes = 3
  min_nodes = 1
  max_nodes = 10
}

module "rds_database" {
  source = "./modules/rds"
  
  identifier = "codex-webdev-${var.environment}"
  engine = "postgres"
  engine_version = "15.4"
  instance_class = "db.t3.micro"
  allocated_storage = 20
  database_name = "app_db"
  username = var.db_username
  password = var.db_password
  vpc_id = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnet_ids
}
```

</details>

## 🧪 Testing Strategy

### Testing Pyramid

```mermaid
graph TD
    subgraph "Testing Pyramid"
        E2E[🎭 E2E Tests<br/>5-10%<br/>Critical User Journeys]
        INT[🔗 Integration Tests<br/>20-30%<br/>API & Component Integration]
        UNIT[⚡ Unit Tests<br/>60-70%<br/>Business Logic & Utils]
    end
    
    subgraph "Testing Tools"
        PW[Playwright<br/>E2E Testing]
        RTL[React Testing Library<br/>Component Testing]
        JEST[Jest<br/>Unit Testing]
        ST[Supertest<br/>API Testing]
    end
    
    E2E --> PW
    INT --> RTL
    INT --> ST
    UNIT --> JEST
    UNIT --> RTL
```

### Test Categories

#### Unit Tests (60-70% Coverage)
- **Business logic** functions and classes
- **Utility functions** and helpers
- **Pure components** without side effects
- **Service layer** methods
- **Repository layer** data access

#### Integration Tests (20-30% Coverage)
- **API endpoints** with database integration
- **Component interactions** with state management
- **Service integrations** with external APIs
- **Database operations** with real data

#### End-to-End Tests (5-10% Coverage)
- **Critical user journeys** (login, purchase, etc.)
- **Cross-browser compatibility** testing
- **Performance testing** for Core Web Vitals
- **Accessibility testing** with assistive technologies

### Testing Best Practices

#### Frontend Testing Example
```typescript
// tests/components/UserProfile.test.tsx
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import { Provider } from 'react-redux';
import { UserProfile } from '@/components/UserProfile';
import { store } from '@/store';
import { server } from '../mocks/server';

// Mock API responses
beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());

describe('UserProfile Component', () => {
  const renderWithProvider = (component: React.ReactElement) => {
    return render(
      <Provider store={store}>
        {component}
      </Provider>
    );
  };

  it('should display user information correctly', async () => {
    renderWithProvider(<UserProfile userId="123" />);
    
    await waitFor(() => {
      expect(screen.getByText('John Doe')).toBeInTheDocument();
      expect(screen.getByText('john.doe@example.com')).toBeInTheDocument();
    });
  });

  it('should handle edit mode correctly', async () => {
    renderWithProvider(<UserProfile userId="123" />);
    
    const editButton = screen.getByRole('button', { name: /edit/i });
    fireEvent.click(editButton);
    
    expect(screen.getByRole('textbox', { name: /first name/i })).toBeInTheDocument();
  });
});
```

#### Backend Testing Example
```typescript
// tests/controllers/user.controller.test.ts
import request from 'supertest';
import { app } from '@/app';
import { prisma } from '@/config/database';

describe('User Controller', () => {
  beforeEach(async () => {
    await prisma.user.deleteMany();
  });

  afterAll(async () => {
    await prisma.$disconnect();
  });

  describe('POST /api/v1/users', () => {
    it('should create a user with valid data', async () => {
      const userData = {
        email: 'test@example.com',
        password: 'Password123!',
        firstName: 'John',
        lastName: 'Doe',
      };

      const response = await request(app)
        .post('/api/v1/users')
        .send(userData)
        .expect(201);

      expect(response.body.success).toBe(true);
      expect(response.body.data.email).toBe(userData.email);
      expect(response.body.data).not.toHaveProperty('password');
    });

    it('should validate required fields', async () => {
      const response = await request(app)
        .post('/api/v1/users')
        .send({})
        .expect(400);

      expect(response.body.success).toBe(false);
      expect(response.body.error).toBe('VALIDATION_ERROR');
    });
  });
});
```

#### E2E Testing Example
```typescript
// tests/e2e/auth.spec.ts
import { test, expect } from '@playwright/test';

test.describe('Authentication Flow', () => {
  test('should allow user to login and access dashboard', async ({ page }) => {
    // Navigate to login page
    await page.goto('/login');
    
    // Fill login form
    await page.fill('[data-testid=email-input]', 'test@example.com');
    await page.fill('[data-testid=password-input]', 'Password123!');
    await page.click('[data-testid=login-button]');
    
    // Verify successful login
    await expect(page).toHaveURL('/dashboard');
    await expect(page.locator('[data-testid=user-menu]')).toBeVisible();
    
    // Check dashboard content
    await expect(page.locator('h1')).toContainText('Dashboard');
  });

  test('should handle login errors gracefully', async ({ page }) => {
    await page.goto('/login');
    
    await page.fill('[data-testid=email-input]', 'invalid@example.com');
    await page.fill('[data-testid=password-input]', 'wrongpassword');
    await page.click('[data-testid=login-button]');
    
    await expect(page.locator('[data-testid=error-message]'))
      .toContainText('Invalid credentials');
  });
});
```

## 🚀 Deployment

### Deployment Strategies

#### Blue-Green Deployment

```mermaid
graph LR
    subgraph "Load Balancer"
        LB[NGINX/ALB]
    end
    
    subgraph "Blue Environment (Current)"
        B1[App Instance 1]
        B2[App Instance 2]
        B3[App Instance 3]
    end
    
    subgraph "Green Environment (New)"
        G1[App Instance 1]
        G2[App Instance 2]
        G3[App Instance 3]
    end
    
    subgraph "Shared Services"
        DB[(Database)]
        REDIS[(Redis)]
        STORAGE[(File Storage)]
    end
    
    LB --> B1
    LB --> B2
    LB --> B3
    
    B1 --> DB
    B2 --> REDIS
    B3 --> STORAGE
    
    G1 -.-> DB
    G2 -.-> REDIS
    G3 -.-> STORAGE
    
    style G1 fill:#90EE90
    style G2 fill:#90EE90
    style G3 fill:#90EE90
```

#### Rolling Deployment

```mermaid
gantt
    title Rolling Deployment Timeline
    dateFormat  X
    axisFormat %s
    
    section Instance 1
    Running     :a1, 0, 30
    Updating    :crit, a2, 30, 40
    Running     :a3, 40, 100
    
    section Instance 2
    Running     :b1, 0, 40
    Updating    :crit, b2, 40, 50
    Running     :b3, 50, 100
    
    section Instance 3
    Running     :c1, 0, 50
    Updating    :crit, c2, 50, 60
    Running     :c3, 60, 100
    
    section Health Checks
    Pre-deploy  :milestone, m1, 0, 0
    Instance 1  :milestone, m2, 40, 40
    Instance 2  :milestone, m3, 50, 50
    Instance 3  :milestone, m4, 60, 60
    Complete    :milestone, m5, 100, 100
```

### Environment Configuration

#### Production Deployment Checklist

- [ ] **Environment Variables** configured securely
- [ ] **Database migrations** applied
- [ ] **SSL certificates** installed and configured
- [ ] **Load balancer** health checks configured
- [ ] **Monitoring & alerting** enabled
- [ ] **Backup strategy** implemented
- [ ] **Security scanning** completed
- [ ] **Performance testing** passed
- [ ] **Rollback plan** prepared

#### Docker Production Setup

<details>
<summary>🐳 Production Dockerfile</summary>

```dockerfile
# Multi-stage production Dockerfile
FROM node:20-alpine AS base
RUN apk add --no-cache libc6-compat
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production && npm cache clean --force

FROM base AS builder
WORKDIR /app
COPY . .
RUN npm ci
RUN npm run build

FROM node:20-alpine AS runner
WORKDIR /app
RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nodejs

COPY --from=builder --chown=nodejs:nodejs /app/dist ./dist
COPY --from=builder --chown=nodejs:nodejs /app/node_modules ./node_modules
COPY --from=builder --chown=nodejs:nodejs /app/package.json ./package.json

USER nodejs
EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD node -e "require('http').get('http://localhost:8000/health', (res) => { process.exit(res.statusCode === 200 ? 0 : 1) }).on('error', () => process.exit(1))"

CMD ["npm", "start"]
```

</details>

### Performance Optimization

#### Frontend Performance Targets

| Metric | Target | Measurement |
|--------|--------|-------------|
| **Largest Contentful Paint (LCP)** | ≤ 2.0s | Core Web Vitals |
| **Interaction to Next Paint (INP)** | ≤ 100ms | User Experience |
| **Cumulative Layout Shift (CLS)** | ≤ 0.1 | Visual Stability |
| **First Contentful Paint (FCP)** | ≤ 1.2s | Loading Performance |
| **Time to Interactive (TTI)** | ≤ 3.0s | Interactivity |

#### Backend Performance Targets

| Metric | Target | Measurement |
|--------|--------|-------------|
| **API Response Time (95th percentile)** | ≤ 200ms | Application Performance |
| **Database Query Time** | ≤ 50ms | Database Performance |
| **Memory Usage** | ≤ 512MB | Resource Utilization |
| **CPU Usage** | ≤ 70% | Resource Utilization |
| **Error Rate** | ≤ 0.1% | Reliability |

## 📚 Documentation

### API Documentation

The project includes comprehensive API documentation using OpenAPI 3.0 specification:

- **Interactive Docs**: http://localhost:8000/docs (Swagger UI)
- **API Spec**: `/docs/openapi.yaml`
- **Postman Collection**: `/docs/postman/`

#### Sample API Endpoints

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|----------------|
| POST | `/api/v1/auth/login` | User authentication | None |
| POST | `/api/v1/auth/refresh` | Refresh JWT tokens | Refresh Token |
| GET | `/api/v1/users` | List users (paginated) | JWT Required |
| POST | `/api/v1/users` | Create new user | Admin Only |
| GET | `/api/v1/users/:id` | Get user by ID | JWT Required |
| PUT | `/api/v1/users/:id` | Update user | Owner/Admin |
| DELETE | `/api/v1/users/:id` | Delete user | Admin Only |

### Architecture Documentation

#### Architecture Decision Records (ADRs)

<details>
<summary>📋 Sample ADR: Database Selection</summary>

```markdown
# ADR-001: Database Selection Strategy

## Status
Accepted

## Context
We need to select appropriate databases for different data types and use cases in our application.

## Decision
We will use a multi-database strategy:
- PostgreSQL for relational data requiring ACID compliance
- MongoDB for document storage and flexible schemas
- Redis for caching and session storage
- Vector databases (Pinecone/Weaviate) for AI/ML applications

## Consequences
### Positive
- Optimal performance for each data type
- Scalability options for different workloads
- Future-proofing for AI/ML integration

### Negative
- Increased operational complexity
- Multiple database skills required
- More complex backup/recovery procedures

## Implementation
- Use Prisma ORM for PostgreSQL
- Use Mongoose for MongoDB
- Use Redis client libraries
- Use vendor SDKs for vector databases
```

</details>

### Component Documentation

Frontend components are documented using Storybook:

```bash
# Start Storybook
npm run storybook

# Build Storybook for production
npm run build-storybook
```

Access at: http://localhost:6006

### Code Documentation Standards

- **JSDoc comments** for all public APIs
- **README files** in each major directory
- **Inline comments** for complex business logic
- **Type definitions** with descriptive names
- **Example usage** in documentation

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

### Quick Contribution Workflow

1. **🍴 Fork the repository**
2. **🌿 Create a feature branch** (`git checkout -b feature/amazing-feature`)
3. **💻 Make your changes** following our coding standards
4. **🧪 Add/update tests** for your changes
5. **✅ Run quality checks** (`npm run lint && npm test`)
6. **📝 Commit your changes** (`git commit -m 'Add amazing feature'`)
7. **🚀 Push to your branch** (`git push origin feature/amazing-feature`)
8. **📋 Open a Pull Request**

### Development Setup for Contributors

```bash
# Clone your fork
git clone https://github.com/your-username/codex-webdev.git
cd codex-webdev

# Add upstream remote
git remote add upstream https://github.com/original-org/codex-webdev.git

# Install dependencies
npm install

# Set up pre-commit hooks
npm run setup:hooks

# Start development environment
npm run dev
```

### Coding Standards

- **Follow the AGENTS.md guidelines** for consistent AI-assisted development
- **Write tests** for all new features and bug fixes
- **Update documentation** when adding new features
- **Use conventional commits** for clear commit history
- **Ensure accessibility** compliance (WCAG 2.2 AA)

### Pull Request Guidelines

- **Keep PRs focused** on a single feature or fix
- **Include tests** and ensure all tests pass
- **Update documentation** as needed
- **Add screenshots** for UI changes
- **Reference relevant issues** in PR description

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Codex WebDev Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE# 🚀 Codex WebDev

> **Enterprise-Grade Web Development Template for 2025**  
> AI-Native • TypeScript-First • Production-Ready • DevSecOps Integrated

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-blue.svg)](https://www.typescriptlang.org/)
[![React](https://img.shields.io/badge/React-18+-61DAFB.svg)](https://reactjs.org/)
[![Node.js](https://img.shields.io/badge/Node.js-20+-green.svg)](https://nodejs.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED.svg)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-1.28+-326CE5.svg)](https://kubernetes.io/)

## 📋 Table of Contents

- [Overview](#overview)
- [🎯 Key Features](#-key-features)
- [🏗️ Architecture](#️-architecture)
- [🛠️ Technology Stack](#️-technology-stack)
- [🚀 Quick Start](#-quick-start)
- [📁 Project Structure](#-project-structure)
- [🤖 AI-Guided Development](#-ai-guided-development)
- [💻 Development Guide](#-development-guide)
- [🔒 Security & DevOps](#-security--devops)
- [🧪 Testing Strategy](#-testing-strategy)
- [🚀 Deployment](#-deployment)
- [📚 Documentation](#-documentation)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

## Overview

**Codex WebDev** is a comprehensive, enterprise-grade web development template designed for 2025's modern development landscape. It combines cutting-edge technologies with AI-native development practices, providing a complete foundation for building scalable, secure, and maintainable web applications.

### 🌟 What Makes This Special?

- **🤖 AI-Native Development**: Unique AGENTS.md system guides AI coding assistants with context-aware instructions
- **🎯 2025-Ready Tech Stack**: Latest versions of React, Node.js, TypeScript, and modern tooling
- **🏗️ Enterprise Architecture**: Production-tested patterns with scalability and maintainability in mind
- **🔒 Security-First**: DevSecOps practices integrated from day one
- **📊 Multi-Database Strategy**: Support for SQL, NoSQL, and Vector databases for AI applications
- **🚀 Performance Optimized**: Core Web Vitals optimization and backend performance best practices

## 🎯 Key Features

### Development Experience
- ✅ **TypeScript Strict Mode** throughout the entire stack
- ✅ **Hot Reloading** with Vite for lightning-fast development
- ✅ **Comprehensive Linting** with ESLint and Prettier
- ✅ **Automated Testing** with Jest, React Testing Library, and Playwright
- ✅ **VS Code Integration** with recommended extensions and settings

### Architecture & Patterns
- ✅ **Layered Architecture** with clear separation of concerns
- ✅ **Repository Pattern** for data access abstraction
- ✅ **Service Layer** for business logic encapsulation
- ✅ **Atomic Design** for component organization
- ✅ **Event-Driven Architecture** with pub/sub patterns

### Production Readiness
- ✅ **Docker Containerization** with multi-stage builds
- ✅ **Kubernetes Orchestration** with helm charts
- ✅ **CI/CD Pipelines** with GitHub Actions
- ✅ **Monitoring & Observability** with OpenTelemetry
- ✅ **Security Scanning** integrated into pipelines

### Database & Storage
- ✅ **PostgreSQL** for relational data with advanced features
- ✅ **MongoDB** for document storage and flexible schemas
- ✅ **Redis** for caching and session management
- ✅ **Vector Databases** (Pinecone/Weaviate) for AI applications

## 🏗️ Architecture

### High-Level System Architecture

```mermaid
graph TB
    subgraph "Client Layer"
        Web[Web Browser]
        Mobile[Mobile App]
    end
    
    subgraph "Frontend Layer"
        React[React App<br/>TypeScript + Vite]
        Store[Redux Toolkit<br/>RTK Query]
        Components[Component Library<br/>Atomic Design]
    end
    
    subgraph "API Gateway"
        Gateway[Express.js Gateway<br/>Auth + Rate Limiting]
    end
    
    subgraph "Backend Services"
        Auth[Auth Service<br/>JWT + OAuth]
        User[User Service<br/>CRUD Operations]
        Business[Business Logic<br/>Domain Services]
    end
    
    subgraph "Data Layer"
        PostgreSQL[(PostgreSQL<br/>Primary Database)]
        MongoDB[(MongoDB<br/>Document Store)]
        Redis[(Redis<br/>Cache + Sessions)]
        Vector[(Vector DB<br/>AI/ML Data)]
    end
    
    subgraph "Infrastructure"
        Docker[Docker Containers]
        K8s[Kubernetes Cluster]
        Monitor[Monitoring<br/>Prometheus + Grafana]
    end
    
    Web --> React
    Mobile --> React
    React <--> Store
    React --> Components
    Store <--> Gateway
    Gateway --> Auth
    Gateway --> User
    Gateway --> Business
    
    Auth --> PostgreSQL
    Auth --> Redis
    User --> PostgreSQL
    User --> MongoDB
    Business --> PostgreSQL
    Business --> Vector
    
    Docker --> K8s
    K8s --> Monitor
```

### Backend Service Architecture

```mermaid
graph LR
    subgraph "Controllers Layer"
        UC[User Controller]
        AC[Auth Controller]
        BC[Business Controller]
    end
    
    subgraph "Middleware"
        Auth[Authentication]
        Valid[Validation]
        Rate[Rate Limiting]
        Log[Logging]
    end
    
    subgraph "Services Layer"
        US[User Service]
        AS[Auth Service]
        ES[Email Service]
        BS[Business Service]
    end
    
    subgraph "Repository Layer"
        UR[User Repository]
        AR[Auth Repository]
        BR[Business Repository]
    end
    
    subgraph "Database Layer"
        PG[(PostgreSQL)]
        MG[(MongoDB)]
        RD[(Redis)]
    end
    
    UC --> Auth
    AC --> Auth
    BC --> Auth
    
    Auth --> Valid
    Valid --> Rate
    Rate --> Log
    
    UC --> US
    AC --> AS
    BC --> BS
    
    US --> UR
    AS --> AR
    BS --> BR
    
    UR --> PG
    AR --> PG
    BR --> MG
    AS --> RD
```

### Frontend Component Hierarchy

```mermaid
graph TD
    subgraph "Application"
        App[App Component]
        Router[React Router]
        Store[Redux Store]
    end
    
    subgraph "Pages"
        Home[Home Page]
        Dashboard[Dashboard Page]
        Profile[Profile Page]
    end
    
    subgraph "Features"
        Auth[Auth Feature]
        UserMgmt[User Management]
        Settings[Settings Feature]
    end
    
    subgraph "Components (Atomic Design)"
        Organisms[Organisms<br/>Header, Sidebar, Forms]
        Molecules[Molecules<br/>SearchBox, Card, Modal]
        Atoms[Atoms<br/>Button, Input, Icon]
    end
    
    subgraph "Shared"
        Hooks[Custom Hooks]
        Utils[Utilities]
        Types[TypeScript Types]
        Services[API Services]
    end
    
    App --> Router
    App --> Store
    Router --> Home
    Router --> Dashboard
    Router --> Profile
    
    Home --> Auth
    Dashboard --> UserMgmt
    Profile --> Settings
    
    Auth --> Organisms
    UserMgmt --> Organisms
    Settings --> Organisms
    
    Organisms --> Molecules
    Molecules --> Atoms
    
    Auth --> Hooks
    UserMgmt --> Services
    Settings --> Utils
```

### Data Flow & Authentication

```mermaid
sequenceDiagram
    participant U as User
    participant F as Frontend
    participant G as API Gateway
    participant A as Auth Service
    participant S as Business Service
    participant D as Database
    participant R as Redis
    
    U->>F: Login Request
    F->>G: POST /auth/login
    G->>A: Validate Credentials
    A->>D: Query User Data
    D-->>A: User Details
    A->>R: Store Session
    A-->>G: JWT Tokens
    G-->>F: Auth Response
    F-->>U: Login Success
    
    Note over U,R: Subsequent API Calls
    
    U->>F: Business Action
    F->>G: API Request + JWT
    G->>G: Verify JWT
    G->>S: Process Request
    S->>D: Data Operation
    D-->>S: Result
    S-->>G: Response
    G-->>F: API Response
    F-->>U: Updated UI
```

### Database Entity Relationships

```mermaid
erDiagram
    USER {
        uuid id PK
        string email UK
        string password_hash
        string first_name
        string last_name
        enum role
        timestamp created_at
        timestamp updated_at
        timestamp deleted_at
    }
    
    SESSION {
        uuid id PK
        uuid user_id FK
        string token UK
        timestamp expires_at
        timestamp created_at
    }
    
    POST {
        uuid id PK
        string title
        text content
        boolean published
        uuid author_id FK
        timestamp created_at
        timestamp updated_at
    }
    
    USER_PREFERENCES {
        uuid id PK
        uuid user_id FK
        jsonb preferences
        timestamp created_at
        timestamp updated_at
    }
    
    USER ||--o{ SESSION : has
    USER ||--o{ POST : creates
    USER ||--|| USER_PREFERENCES : has
```

## 🛠️ Technology Stack

### Frontend Technologies

| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| React | 18+ | UI Framework | [React Docs](https://reactjs.org/) |
| TypeScript | 5.0+ | Type Safety | [TS Docs](https://www.typescriptlang.org/) |
| Vite | 5+ | Build Tool | [Vite Docs](https://vitejs.dev/) |
| Material UI | 5+ | UI Components | [MUI Docs](https://mui.com/) |
| Redux Toolkit | Latest | State Management | [RTK Docs](https://redux-toolkit.js.org/) |
| React Router | 6+ | Routing | [Router Docs](https://reactrouter.com/) |
| React Testing Library | Latest | Component Testing | [RTL Docs](https://testing-library.com/) |
| Playwright | Latest | E2E Testing | [Playwright Docs](https://playwright.dev/) |

### Backend Technologies

| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Node.js | 20+ | Runtime Environment | [Node.js Docs](https://nodejs.org/) |
| Express.js | 4.18+ | Web Framework | [Express Docs](https://expressjs.com/) |
| TypeScript | 5.0+ | Type Safety | [TS Docs](https://www.typescriptlang.org/) |
| Prisma | Latest | Database ORM | [Prisma Docs](https://www.prisma.io/) |
| JWT | Latest | Authentication | [JWT.io](https://jwt.io/) |
| Zod | Latest | Validation | [Zod Docs](https://zod.dev/) |
| Jest | Latest | Unit Testing | [Jest Docs](https://jestjs.io/) |
| Supertest | Latest | API Testing | [Supertest](https://github.com/visionmedia/supertest) |

### Database Technologies

| Database | Use Case | Features |
|----------|----------|----------|
| PostgreSQL 15+ | Primary relational data | ACID compliance, JSON support, full-text search |
| MongoDB 7+ | Document storage | Flexible schemas, aggregation pipelines |
| Redis 7+ | Caching & sessions | High performance, pub/sub, clustering |
| Pinecone/Weaviate | Vector storage | AI embeddings, semantic search |

### Infrastructure & DevOps

| Technology | Purpose | Configuration |
|------------|---------|---------------|
| Docker | Containerization | Multi-stage builds |
| Kubernetes | Orchestration | Helm charts included |
| GitHub Actions | CI/CD | Automated testing & deployment |
| Terraform | Infrastructure as Code | Multi-cloud support |
| Prometheus | Monitoring | Metrics collection |
| Grafana | Visualization | Custom dashboards |

## 🚀 Quick Start

### Prerequisites

Ensure you have the following installed:

- **Node.js** 20+ ([Download](https://nodejs.org/))
- **Docker** & Docker Compose ([Download](https://www.docker.com/))
- **Git** ([Download](https://git-scm.com/))
- **PostgreSQL** 15+ (or use Docker)
- **Redis** 7+ (or use Docker)

### 1. Clone & Setup

```bash
# Clone the repository
git clone https://github.com/your-org/codex-webdev.git
cd codex-webdev

# Install dependencies
npm install

# Copy environment files
cp frontend/.env.example frontend/.env
cp backend/.env.example backend/.env
```

### 2. Configure Environment

```bash
# Edit backend environment
nano backend/.env
```

<details>
<summary>📋 Backend Environment Variables</summary>

```env
NODE_ENV=development
PORT=8000

# Database
DATABASE_URL=postgresql://postgres:password@localhost:5432/app_db

# Redis
REDIS_URL=redis://localhost:6379

# JWT Keys (generate with openssl)
JWT_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----..."
JWT_PUBLIC_KEY="-----BEGIN PUBLIC KEY-----..."

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-password

# CORS
CORS_ORIGINS=http://localhost:3000
```

</details>

### 3. Start Development Environment

```bash
# Option 1: Docker Compose (Recommended)
docker-compose up -d

# Option 2: Local Development
npm run dev:services    # Start databases
npm run dev            # Start both frontend and backend
```

### 4. Initialize Database

```bash
# Run database migrations
npm run db:migrate

# Seed development data
npm run db:seed
```

### 5. Verify Installation

Navigate to:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8000
- **API Health**: http://localhost:8000/health

### 6. Run Tests

```bash
# Run all tests
npm test

# Run specific test suites
npm run test:unit        # Unit tests
npm run test:integration # Integration tests
npm run test:e2e        # End-to-end tests
```

## 📁 Project Structure

```
codex-webdev/
├── 📁 frontend/                 # React TypeScript application
│   ├── 📁 src/
│   │   ├── 📁 components/       # UI components (atomic design)
│   │   │   ├── 📁 atoms/        # Basic elements (Button, Input)
│   │   │   ├── 📁 molecules/    # Composed components (SearchBox)
│   │   │   └── 📁 organisms/    # Complex components (Header, Form)
│   │   ├── 📁 features/         # Feature-based organization
│   │   │   ├── 📁 auth/         # Authentication feature
│   │   │   ├── 📁 dashboard/    # Dashboard feature
│   │   │   └── 📁 profile/      # User profile feature
│   │   ├── 📁 hooks/           # Custom React hooks
│   │   ├── 📁 pages/           # Route components
│   │   ├── 📁 services/        # API integration
│   │   ├── 📁 store/           # Redux store & slices
│   │   ├── 📁 types/           # TypeScript definitions
│   │   ├── 📁 utils/           # Utility functions
│   │   └── 📁 assets/          # Static assets
│   ├── 📁 tests/               # Frontend tests
│   ├── 📄 vite.config.ts       # Vite configuration
│   ├── 📄 tsconfig.json        # TypeScript config
│   └── 📄 AGENTS.md            # Frontend AI guidance
│
├── 📁 backend/                  # Node.js Express API
│   ├── 📁 src/
│   │   ├── 📁 controllers/      # Route handlers
│   │   ├── 📁 services/         # Business logic
│   │   ├── 📁 repositories/     # Data access layer
│   │   ├── 📁 models/           # Data models
│   │   ├── 📁 middleware/       # Express middleware
│   │   ├── 📁 routes/           # API route definitions
│   │   ├── 📁 config/           # Configuration management
│   │   ├── 📁 types/            # TypeScript definitions
│   │   ├── 📁 utils/            # Utility functions
│   │   ├── 📄 app.ts            # Express app setup
│   │   └── 📄 server.ts         # Server initialization
│   ├── 📁 tests/               # Backend tests
│   ├── 📁 migrations/          # Database migrations
│   ├── 📄 Dockerfile           # Container definition
│   ├── 📄 tsconfig.json        # TypeScript config
│   └── 📄 AGENTS.md            # Backend AI guidance
│
├── 📁 database/                 # Database configurations
│   └── 📄 AGENTS.md            # Database AI guidance
│
├── 📁 infrastructure/           # DevOps configurations
│   ├── 📁 devops/
│   │   ├── 📁 k8s/             # Kubernetes manifests
│   │   ├── 📁 terraform/       # Infrastructure as Code
│   │   ├── 📁 monitoring/      # Observability configs
│   │   └── 📄 AGENTS.md        # DevOps AI guidance
│   └── 📁 docker/              # Docker configurations
│
├── 📁 docs/                     # Documentation
│   ├── 📄 api.md               # API documentation
│   ├── 📄 architecture.md      # Architecture decisions
│   └── 📄 deployment.md        # Deployment guide
│
├── 📁 scripts/                  # Build & deployment scripts
│   ├── 📄 setup.sh             # Initial setup
│   ├── 📄 deploy.sh            # Deployment script
│   └── 📄 test.sh              # Testing script
│
├── 📁 shared/                   # Shared types & utilities
│   ├── 📄 types.ts             # Common TypeScript types
│   └── 📄 constants.ts         # Shared constants
│
├── 📄 .codex/AGENTS.md         # Global AI guidance
├── 📄 AGENTS.md                # Project-level AI guidance
├── 📄 docker-compose.yml       # Local development setup
├── 📄 package.json             # Root package configuration
├── 📄 README.md                # This file
└── 📄 LICENSE                  # MIT License
```

### Key Directory Purposes

| Directory | Purpose | Key Files |
|-----------|---------|-----------|
| `frontend/` | React application with TypeScript | `src/`, `tests/`, `vite.config.ts` |
| `backend/` | Express.js API server | `src/`, `tests/`, `Dockerfile` |
| `database/` | Database schemas and guidelines | `AGENTS.md`, schema definitions |
| `infrastructure/` | DevOps and deployment configs | `k8s/`, `terraform/`, monitoring |
| `docs/` | Project documentation | API docs, architecture, guides |
| `scripts/` | Automation and build scripts | Setup, deployment, testing |
| `shared/` | Common types and utilities | TypeScript definitions |

## 🤖 AI-Guided Development

### The AGENTS.md System

Codex WebDev features a **revolutionary hierarchical guidance system** for AI coding assistants. The AGENTS.md files provide context-aware instructions that help AI tools understand your project's architecture, conventions, and best practices.

```mermaid
graph TD
    subgraph "AGENTS.md Hierarchy"
        Global["🌍 ~/.codex/AGENTS.md<br/>Global Preferences"]
        Project["📁 /AGENTS.md<br/>Project Guidelines"]
        Frontend["⚛️ /frontend/AGENTS.md<br/>React + TypeScript"]
        Backend["🔧 /backend/AGENTS.md<br/>Node.js + Express"]
        Database["🗄️ /database/AGENTS.md<br/>Multi-DB Strategy"]
        DevOps["🚀 /infrastructure/devops/AGENTS.md<br/>K8s + Security"]
    end
    
    Global --> Project
    Project --> Frontend
    Project --> Backend
    Project --> Database
    Project --> DevOps
    
    Frontend --> Components["Component Development"]
    Backend --> Services["Service Architecture"]
    Database --> Schemas["Schema Design"]
    DevOps --> Deployment["Deployment Automation"]
```

### How to Use AGENTS.md Files

#### 1. **Setup Your Global Preferences**
```bash
# Create global AI guidance
mkdir -p ~/.codex
cp .codex/AGENTS.md ~/.codex/
# Edit with your personal preferences
```

#### 2. **Configure Project-Specific Guidelines**
The root `AGENTS.md` contains project-wide standards that AI assistants will follow when working on any part of your application.

#### 3. **Technology-Specific Instructions**
Each technology stack has its own AGENTS.md with detailed guidance:

- **Frontend**: React patterns, component architecture, state management
- **Backend**: Express patterns, service layer design, API conventions
- **Database**: Schema design, query optimization, migration strategies
- **DevOps**: Security practices, deployment automation, monitoring

#### 4. **AI Assistant Integration**

<details>
<summary>🤖 GitHub Copilot Integration</summary>

```json
// .vscode/settings.json
{
  "github.copilot.enable": {
    "*": true,
    "yaml": true,
    "plaintext": false,
    "markdown": true
  },
  "github.copilot.advanced": {
    "length": 500,
    "temperature": 0.1
  }
}
```

</details>

<details>
<summary>🧠 Claude/ChatGPT Integration</summary>

When starting a new coding session:

1. Share the relevant AGENTS.md file(s)
2. Specify your current task context
3. Request code that follows the established patterns

Example prompt:
```
I'm working on the user authentication feature. Please review /backend/AGENTS.md 
and /frontend/AGENTS.md, then help me implement JWT refresh token logic following 
the established patterns.
```

</details>

###
