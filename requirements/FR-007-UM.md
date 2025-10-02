# FR-UM-007: User Management and Access Control

## Requirement
The system shall implement comprehensive user management and access control in compliance with Indonesian data privacy regulations and OJK security requirements.

## Functional Requirements

### 1. User Authentication
- **FR-UM-007.1**: System must provide secure user authentication:
  - Multi-factor authentication (MFA) support
  - Password complexity requirements (minimum 12 characters)
  - Account lockout after failed attempts (5 attempts)
  - Session timeout management (30 minutes inactivity)
  - Single Sign-On (SSO) integration capability
  - Indonesian national ID verification option

### 2. Role-Based Access Control (RBAC)
- **FR-UM-007.2**: System must implement role-based access control:
  - **Compliance Officer**: Full access to alerts, cases, and reporting
  - **Compliance Manager**: Oversight and approval authority
  - **Investigation Officer**: Case investigation and evidence collection
  - **Reporting Officer**: Regulatory filing and report generation
  - **System Administrator**: System configuration and user management
  - **Auditor**: Read-only access for audit purposes
  - **Executive**: Dashboard and summary reporting access

### 3. User Lifecycle Management
- **FR-UM-007.3**: System must manage complete user lifecycle:
  - User registration and onboarding with documentation
  - Role assignment based on job function
  - Access request and approval workflow
  - Regular access reviews and certification
  - User suspension and termination procedures
  - Emergency access procedures for critical situations

### 4. Permission Management
- **FR-UM-007.4**: System must provide granular permission control:
  - Functional access (view, create, edit, delete)
  - Data access restrictions (customer segmentation)
  - Transaction amount limits based on role
  - Geographic access restrictions
  - Time-based access restrictions
  - Approval hierarchy enforcement

### 5. Indonesian Regulatory Compliance
- **FR-UM-007.5**: System must comply with Indonesian regulations:
  - Personal data protection (PDP Law preparation)
  - OJK cybersecurity requirements
  - Data localization requirements
  - Indonesian language interface option
  - Local user identification integration
  - Regulatory audit trail compliance

### 6. Security Monitoring
- **FR-UM-007.6**: System must provide security monitoring capabilities:
  - Real-time suspicious activity detection
  - Failed login attempt monitoring
  - Privileged access monitoring
  - Data access pattern analysis
  - Security incident reporting
  - Integration with SIEM systems

### 7. Training and Certification
- **FR-UM-007.7**: System must track user training and certification:
  - AML compliance training records
  - Regulatory knowledge assessment
  - Security awareness training
  - Role-specific competency validation
  - Training expiration tracking
  - Certification document management

## User Roles and Responsibilities

### Compliance Department
- **Compliance Officer**: Daily AML operations and alert management
- **Compliance Manager**: Department oversight and regulatory reporting
- **Investigation Officer**: Case investigation and evidence collection
- **Reporting Officer**: PPATK and OJK report preparation

### IT and Operations
- **System Administrator**: System configuration and maintenance
- **Security Officer**: Security monitoring and incident response
- **Database Administrator**: Data management and backup operations

### Management
- **Executive Management**: Dashboard access and strategic oversight
- **Risk Manager**: Risk assessment and monitoring
- **Internal Auditor**: Compliance audit and control testing

## Access Control Matrix

| Function | Compliance Officer | Compliance Manager | Investigation Officer | Reporting Officer | System Administrator | Auditor |
|----------|-------------------|-------------------|----------------------|-------------------|----------------------|---------|
| Customer Management | View/Edit | View/Edit | View/Edit | View | Full Access | View |
| Transaction Monitoring | Full Access | Full Access | View | View | View Only | View |
| Alert Management | Full Access | Full Access | Full Access | View | View Only | View |
| Case Investigation | Full Access | Approve | Full Access | View | View Only | View |
| Regulatory Reporting | Prepare | Approve | View | Full Access | View Only | View |
| System Configuration | View | View | View | View | Full Access | View |
| Audit Trail | View | View | View | View | View | Full Access |

## Security Requirements
- **Password Policy**: Minimum 12 characters, complexity requirements
- **MFA**: Required for all users
- **Session Timeout**: 30 minutes of inactivity
- **Account Lockout**: 5 failed attempts, 15-minute lockout
- **Password Rotation**: 90-day password change requirement
- **Access Review**: Quarterly access certification

## Compliance References
- Peraturan OJK No. 12/POJK.01/2017 Pasal 43-46
- Peraturan OJK No. 23/POJK.01/2019 Pasal 41-44
- Standar Keamanan Siber OJK
- Undang-Undang Nomor 8 Tahun 2010 Pasal 35-38
- Draft RUU PDP (Personal Data Protection)

## Data Retention
- User access logs: 2 years minimum
- Training records: 5 years minimum
- Certification documents: 5 years minimum
- Access approval records: 7 years minimum
- Security incident logs: 10 years minimum