# AML Application - Architecture Overview

## High-Level Architecture

```mermaid
graph TB
    subgraph "Client Layer"
        U[Web Browser]
        M[Mobile App]
        A[Admin Dashboard]
    end

    subgraph "Web Application Layer"
        W[Spring Boot<br/>Web Application]
        T[Thymeleaf Templates]
        S[Spring Security]
        V[Validation Layer]
    end

    subgraph "Business Logic Layer"
        CS[Customer Service]
        TS[Transaction Service]
        SS[Screening Service]
        CMS[Case Management Service]
        RS[Reporting Service]
        AS[Audit Service]
        US[User Management Service]
    end

    subgraph "Data Access Layer"
        R[Spring Data JPA]
        H[Hibernate ORM]
        C[Connection Pooling]
        M[Cache Manager]
    end

    subgraph "Database Layer"
        P[(PostgreSQL<br/>Primary Database)]
        R2[Redis<br/>Cache]
        E[Elasticsearch<br/>Search]
    end

    subgraph "External Integration Layer"
        PP[PPATK API]
        OJ[OJK API]
        BI[Bank Indonesia API]
        DU[DUKCAPIL API]
        CB[Core Banking API]
        SN[SNAP Payment API]
    end

    subgraph "External Services"
        W1[OFAC Sanctions]
        W2[UN Sanctions]
        W3[PEP Database]
        W4[Adverse Media]
    end

    subgraph "Infrastructure"
        D[Docker]
        K[Kubernetes]
        M2[Monitoring]
        L[Logging]
        B[Backup]
    end

    U --> W
    M --> W
    A --> W
    W --> T
    W --> S
    W --> V

    W --> CS
    W --> TS
    W --> SS
    W --> CMS
    W --> RS
    W --> AS
    W --> US

    CS --> R
    TS --> R
    SS --> R
    CMS --> R
    RS --> R
    AS --> R
    US --> R

    R --> H
    R --> C
    C --> M
    M --> R2
    R --> P
    R --> E

    CS --> PP
    TS --> CB
    SS --> W1
    SS --> W2
    SS --> W3
    SS --> W4
    RS --> PP
    RS --> OJ
    RS --> BI
    CS --> DU
    TS --> SN

    P --> B
    W --> L
    W --> M2
    W --> D
```

## Component Architecture

### 1. Presentation Layer (Spring MVC + Thymeleaf)

```mermaid
graph TB
    subgraph "Web Controllers"
        CC[CustomerController]
        TC[TransactionController]
        SC[ScreeningController]
        CMC[CaseManagementController]
        RC[ReportingController]
        UC[UserController]
        AC[AuditController]
    end

    subgraph "View Templates"
        CT[Customer Templates]
        TT[Transaction Templates]
        ST[Screening Templates]
        CMT[Case Templates]
        RT[Reporting Templates]
        UT[User Templates]
        AT[Audit Templates]
    end

    subgraph "Web Configuration"
        WC[WebConfig]
        SC[SecurityConfig]
        VC[ValidationConfig]
        MC[MessageConfig]
    end

    CC --> CT
    TC --> TT
    SC --> ST
    CMC --> CMT
    RC --> RT
    UC --> UT
    AC --> AT

    WC --> CC
    WC --> TC
    WC --> SC
    WC --> CMC
    WC --> RC
    WC --> UC
    WC --> AC

    SC --> CC
    SC --> TC
    SC --> SC
    SC --> CMC
    SC --> RC
    SC --> UC
    SC --> AC
```

### 2. Service Layer Architecture

```mermaid
graph TB
    subgraph "Core Services"
        CS[CustomerService]
        TS[TransactionService]
        SS[ScreeningService]
        CMS[CaseManagementService]
        RS[ReportingService]
        AS[AuditService]
        US[UserService]
    end

    subgraph "Integration Services"
        PS[PpatkService]
        OS[OjkService]
        DS[DukcapilService]
        BS[BankingService]
        WS[WatchlistService]
        NS[NotificationService]
    end

    subgraph "Business Rules"
        RE[RuleEngine]
        RS[RiskScoringEngine]
        FS[FuzzyMatchingEngine]
        AE[AlertEngine]
        CE[ComplianceEngine]
    end

    subgraph "Utilities"
        VS[ValidationService]
        ES[EncryptionService]
 LS[LoggingService]
        MS[MonitoringService]
        CS2[CacheService]
    end

    CS --> PS
    CS --> DS
    CS --> VS
    CS --> RS

    TS --> BS
    TS --> AE
    TS --> CS2

    SS --> WS
    SS --> FS
    SS --> VS

    CMS --> RS
    CMS --> NS
    CMS --> VS

    RS --> PS
    RS --> OS
    RS --> CE

    AS --> LS
    AS --> MS

    US --> VS
    US --> ES

    RE --> TS
    RE --> SS
    RE --> CMS
```

### 3. Data Access Layer Architecture

```mermaid
graph TB
    subgraph "Repositories"
        CR[CustomerRepository]
        TR[TransactionRepository]
        AR[AlertRepository]
        IR[InvestigationCaseRepository]
        RR[RegulatoryReportRepository]
        UR[UserRepository]
        ALR[AuditLogRepository]
    end

    subgraph "JPA Configuration"
        EC[Entity Configuration]
        QC[Query Configuration]
        TC[Transaction Configuration]
        CC[Cache Configuration]
    end

    subgraph "Database Connection"
        CP[Connection Pool]
        DS[DataSource]
        TM[Transaction Manager]
        EM[Entity Manager]
    end

    subgraph "Database Schema"
        CS[Customer Schema]
        TS[Transaction Schema]
        AS[Audit Schema]
        US[User Schema]
        CS2[Configuration Schema]
    end

    CR --> EC
    TR --> EC
    AR --> EC
    IR --> EC
    RR --> EC
    UR --> EC
    ALR --> EC

    EC --> QC
    EC --> TC
    EC --> CC

    QC --> CP
    TC --> TM
    CC --> CS2

    CP --> DS
    TM --> EM
    EM --> CS
    EM --> TS
    EM --> AS
    EM --> US
    EM --> CS2
```

### 4. Security Architecture

```mermaid
graph TB
    subgraph "Authentication"
        L[Login Controller]
        P[Provider Manager]
        U[UserDetailsService]
        T[Token Service]
        M[MFA Service]
    end

    subgraph "Authorization"
        V[Voter System]
        R[Role Hierarchy]
        P2[Permission Checker]
        A[Access Control]
    end

    subgraph "Security Filters"
        AF[Authentication Filter]
        AF2[Authorization Filter]
        CF[CSRF Filter]
        SF[Security Filter]
    end

    subgraph "Data Protection"
        E[Encryption Service]
        D[Data Masking]
        A2[Audit Service]
        K[Key Management]
    end

    subgraph "Compliance"
        RL[Regulatory Logging]
        DP[Data Privacy]
        AC[Access Control]
        RR[Retention Rules]
    end

    L --> P
    P --> U
    P --> T
    T --> M

    M --> V
    V --> P2
    P2 --> A

    A --> AF
    A --> AF2
    AF --> CF
    AF2 --> SF

    A --> E
    E --> D
    E --> K
    E --> A2

    A2 --> RL
    RL --> DP
    DP --> AC
    AC --> RR
```

### 5. Integration Architecture

```mermaid
graph TB
    subgraph "API Gateway"
        G[API Gateway]
        R[Router]
        F[Filter]
        L[Load Balancer]
    end

    subgraph "External APIs"
        PP[PPATK API]
        OJ[OJK API]
        BI[Bank Indonesia API]
        DU[DUKCAPIL API]
        CB[Core Banking API]
        SN[SNAP API]
    end

    subgraph "Message Queue"
        MQ[RabbitMQ]
        T[Topics]
        Q[Queues]
        E[Exchanges]
    end

    subgraph "Webhooks"
        W[Webhook Handler]
        E2[Event Processor]
        N[Notification Service]
        A2[Audit Service]
    end

    subgraph "Integration Clients"
        PC[PPATK Client]
        OC[OJK Client]
        BC[Banking Client]
        DC[Dukcapil Client]
        WC[Watchlist Client]
    end

    G --> R
    R --> F
    F --> L

    PC --> PP
    OC --> OJ
    BC --> CB
    DC --> DU
    WC --> SN

    PC --> MQ
    OC --> MQ
    BC --> MQ
    DC --> MQ

    MQ --> T
    T --> Q
    Q --> E

    E --> W
    W --> E2
    E2 --> N
    E2 --> A2
```

### 6. Monitoring and Observability Architecture

```mermaid
graph TB
    subgraph "Application Monitoring"
        M[Metrics Collector]
        H[Health Check]
        T[Tracing]
        L[Logging]
    end

    subgraph "Infrastructure Monitoring"
        C[CPU/Memory]
        D[Disk I/O]
        N[Network]
        DB[Database]
    end

    subgraph "Business Monitoring"
        A[Alert Metrics]
        T2[Transaction Metrics]
        C[Case Metrics]
        R[Report Metrics]
    end

    subgraph "Alerting"
        EA[Email Alerts]
        SA[SMS Alerts]
        PA[Push Notifications]
        DA[Dashboard Alerts]
    end

    subgraph "Visualization"
        D2[Dashboard]
        G[Graphs]
        R2[Reports]
        A3[Analytics]
    end

    subgraph "Compliance Monitoring"
        RL[Regulatory Logs]
        AL[Audit Trails]
        PL[Performance Logs]
        EL[Error Logs]
    end

    M --> H
    M --> T
    M --> L

    C --> M
    D --> M
    N --> M
    DB --> M

    A --> M
    T2 --> M
    C --> M
    R --> M

    M --> EA
    M --> SA
    M --> PA
    M --> DA

    M --> D2
    M --> G
    M --> R2
    M --> A3

    L --> RL
    L --> AL
    L --> PL
    L --> EL
```

## Deployment Architecture

### Docker Compose Configuration

```mermaid
graph TB
    subgraph "Application Services"
        A1[AML Application]
        N[Nginx Reverse Proxy]
        R[Redis Cache]
    end

    subgraph "Database Services"
        P[PostgreSQL]
        E[Elasticsearch]
    end

    subgraph "Message Queue"
        Q[RabbitMQ]
    end

    subgraph "Monitoring"
        M[Prometheus]
        G[Grafana]
        L[Logstash]
    end

    subgraph "Networking"
        NW[Network]
        LB[Load Balancer]
        FW[Firewall]
    end

    NW --> LB
    LB --> FW
    FW --> A1
    FW --> N

    A1 --> P
    A1 --> R
    A1 --> E
    A1 --> Q

    Q --> A1
    R --> A1

    M --> A1
    M --> P
    M --> Q
    G --> M
    L --> A1
```

This comprehensive architecture overview provides a detailed design for the AML application, covering all layers from presentation to infrastructure, with specific attention to Indonesian regulatory requirements and PPATK integration.