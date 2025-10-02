# AML Application - Database Schema

## Main Entities and Relationships

```mermaid
erDiagram
    CUSTOMER ||--o{ CUSTOMER_DOCUMENT : has
    CUSTOMER ||--o{ TRANSACTION : performs
    CUSTOMER ||--o{ RISK_ASSESSMENT : has
    CUSTOMER ||--o{ SCREENING_RESULT : has
    CUSTOMER ||--|| DUKCAPIL_VERIFICATION : has
    CUSTOMER ||--o{ INVESTIGATION_CASE : involved_in

    TRANSACTION ||--o{ ALERT : triggers
    TRANSACTION ||--o{ REGULATORY_REPORT : included_in

    ALERT ||--|| INVESTIGATION_CASE : leads_to
    INVESTIGATION_CASE ||--o{ CASE_EVIDENCE : contains
    INVESTIGATION_CASE ||--o{ REGULATORY_REPORT : results_in

    USER ||--o{ AUDIT_LOG : performs
    USER ||--o{ INVESTIGATION_CASE : assigned_to
    USER ||--o{ USER_ROLE : has
    USER ||--o{ USER_TRAINING : completes

    REGULATORY_REPORT ||--|| PPATK_SUBMISSION : submitted_to

    WATCHLIST_ENTRY ||--o{ SCREENING_RESULT : matched_with

    COMPLIANCE_RULE ||--o{ ALERT : triggers

    ROLE ||--o{ USER_ROLE : assigned_to
    ROLE ||--o{ ROLE_PERMISSION : has
    PERMISSION ||--o{ ROLE_PERMISSION : belongs_to

    TRAINING ||--o{ USER_TRAINING : required_by

    CUSTOMER {
        BIGINT id PK
        VARCHAR(100) ktp_number UK
        VARCHAR(200) full_name NOT NULL
        DATE date_of_birth NOT NULL
        VARCHAR(100) place_of_birth
        TEXT address NOT NULL
        VARCHAR(20) phone
        VARCHAR(100) email
        VARCHAR(100) occupation
        VARCHAR(500) source_of_funds
        VARCHAR(20) risk_level NOT NULL
        DECIMAL expected_monthly_volume
        VARCHAR(100) customer_type NOT NULL
        BOOLEAN is_pep NOT NULL DEFAULT FALSE
        BOOLEAN is_active NOT NULL DEFAULT TRUE
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        TIMESTAMP updated_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT created_by
        BIGINT updated_by
    }

    CUSTOMER_DOCUMENT {
        BIGINT id PK
        BIGINT customer_id FK NOT NULL
        VARCHAR(50) document_type NOT NULL
        VARCHAR(255) file_name NOT NULL
        VARCHAR(500) file_path NOT NULL
        DATE upload_date NOT NULL
        DATE expiry_date
        BOOLEAN is_verified NOT NULL DEFAULT FALSE
        TIMESTAMP verified_at
        BIGINT verified_by
        TEXT verification_notes
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    TRANSACTION {
        BIGINT id PK
        VARCHAR(100) transaction_id UK NOT NULL
        BIGINT customer_id FK NOT NULL
        DECIMAL amount NOT NULL
        VARCHAR(3) currency NOT NULL
        VARCHAR(50) transaction_type NOT NULL
        TIMESTAMP transaction_date NOT NULL
        TEXT description
        VARCHAR(50) source_account
        VARCHAR(50) destination_account
        VARCHAR(20) status NOT NULL
        VARCHAR(100) branch_code
        VARCHAR(100) channel
        VARCHAR(100) location
        VARCHAR(10) country_code
        DECIMAL amount_idr
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    ALERT {
        BIGINT id PK
        VARCHAR(50) alert_id UK NOT NULL
        BIGINT customer_id FK NOT NULL
        BIGINT transaction_id FK
        VARCHAR(50) alert_type NOT NULL
        VARCHAR(20) severity NOT NULL
        TEXT description NOT NULL
        TIMESTAMP generated_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        VARCHAR(20) status NOT NULL
        BIGINT rule_id FK
        DECIMAL risk_score
        TEXT rule_triggered
        BOOLEAN is_high_priority NOT NULL DEFAULT FALSE
        TIMESTAMP reviewed_at
        BIGINT reviewed_by
        TEXT review_notes
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    INVESTIGATION_CASE {
        BIGINT id PK
        VARCHAR(50) case_number UK NOT NULL
        BIGINT customer_id FK NOT NULL
        BIGINT alert_id FK NOT NULL
        VARCHAR(20) status NOT NULL
        BIGINT assigned_officer_id FK
        DATE created_date NOT NULL
        DATE due_date
        DATE closed_date
        VARCHAR(50) decision
        TEXT summary
        TEXT decision_justification
        BOOLEAN requires_escalation NOT NULL DEFAULT FALSE
        TIMESTAMP escalated_at
        BIGINT escalated_by
        TEXT escalation_reason
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT created_by
        TIMESTAMP updated_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT updated_by
    }

    CASE_EVIDENCE {
        BIGINT id PK
        BIGINT case_id FK NOT NULL
        VARCHAR(50) evidence_type NOT NULL
        VARCHAR(255) file_name
        VARCHAR(500) file_path
        TIMESTAMP uploaded_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        TEXT description
        BIGINT uploaded_by FK NOT NULL
        TEXT metadata
    }

    SCREENING_RESULT {
        BIGINT id PK
        BIGINT customer_id FK NOT NULL
        VARCHAR(50) screening_type NOT NULL
        BOOLEAN is_match NOT NULL
        DECIMAL confidence_score
        VARCHAR(255) matched_name
        VARCHAR(100) watchlist_name
        TIMESTAMP screened_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BOOLEAN is_false_positive NOT NULL DEFAULT FALSE
        TIMESTAMP reviewed_at
        BIGINT reviewed_by
        TEXT review_notes
        TEXT match_details
    }

    REGULATORY_REPORT {
        BIGINT id PK
        VARCHAR(50) report_number UK NOT NULL
        VARCHAR(50) report_type NOT NULL
        VARCHAR(20) status NOT NULL
        DATE generated_date NOT NULL
        DATE submitted_date
        VARCHAR(100) submission_id
        VARCHAR(100) reference_number
        BIGINT case_id FK
        TEXT report_content
        TEXT submission_response
        BOOLEAN is_acknowledged NOT NULL DEFAULT FALSE
        TIMESTAMP acknowledged_at
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT created_by
    }

    PPATK_SUBMISSION {
        BIGINT id PK
        BIGINT report_id FK NOT NULL
        VARCHAR(100) submission_id UK NOT NULL
        VARCHAR(20) submission_status NOT NULL
        TIMESTAMP submitted_at NOT NULL
        TIMESTAMP acknowledged_at
        VARCHAR(100) reference_number
        TEXT response_message
        TEXT error_details
        INTEGER retry_count NOT NULL DEFAULT 0
        TIMESTAMP next_retry_at
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    USER {
        BIGINT id PK
        VARCHAR(100) username UK NOT NULL
        VARCHAR(100) email UK NOT NULL
        VARCHAR(200) full_name NOT NULL
        VARCHAR(255) password_hash NOT NULL
        VARCHAR(100) employee_id
        VARCHAR(50) department
        BOOLEAN is_active NOT NULL DEFAULT TRUE
        TIMESTAMP last_login
        BOOLEAN mfa_enabled NOT NULL DEFAULT FALSE
        VARCHAR(100) mfa_secret
        TEXT mfa_backup_codes
        BOOLEAN force_password_change NOT NULL DEFAULT FALSE
        TIMESTAMP password_expires_at
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT created_by
        TIMESTAMP updated_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT updated_by
    }

    AUDIT_LOG {
        BIGINT id PK
        VARCHAR(100) user_id
        VARCHAR(50) action NOT NULL
        VARCHAR(50) object_type
        VARCHAR(100) object_id
        TEXT details
        TIMESTAMP timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP
        VARCHAR(45) ip_address
        VARCHAR(500) user_agent
        VARCHAR(20) status
        TEXT error_message
    }

    RISK_ASSESSMENT {
        BIGINT id PK
        BIGINT customer_id FK NOT NULL
        VARCHAR(20) overall_risk NOT NULL
        TEXT risk_factors
        DATE assessed_date NOT NULL
        BIGINT assessed_by FK NOT NULL
        VARCHAR(100) methodology
        DATE next_review_date
        TEXT assessment_notes
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    WATCHLIST_ENTRY {
        BIGINT id PK
        VARCHAR(255) name NOT NULL
        VARCHAR(50) entity_type NOT NULL
        TEXT aliases
        DATE date_of_birth
        VARCHAR(100) nationality
        VARCHAR(50) watchlist_type NOT NULL
        DATE added_date NOT NULL
        DATE last_updated
        BOOLEAN is_active NOT NULL DEFAULT TRUE
        TEXT additional_info
        TEXT metadata
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    COMPLIANCE_RULE {
        BIGINT id PK
        VARCHAR(100) rule_name UK NOT NULL
        TEXT description
        VARCHAR(50) rule_type NOT NULL
        TEXT condition
        DECIMAL threshold
        BOOLEAN is_active NOT NULL DEFAULT TRUE
        DATE effective_date
        DATE expiry_date
        TEXT rule_parameters
        INTEGER priority NOT NULL DEFAULT 1
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT created_by
        TIMESTAMP updated_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT updated_by
    }

    DUKCAPIL_VERIFICATION {
        BIGINT id PK
        BIGINT customer_id FK NOT NULL
        VARCHAR(100) ktp_number NOT NULL
        VARCHAR(20) verification_status NOT NULL
        TIMESTAMP verified_at
        TEXT response_message
        VARCHAR(100) dukcapil_reference
        TEXT verification_data
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    ROLE {
        BIGINT id PK
        VARCHAR(50) role_name UK NOT NULL
        TEXT description
        BOOLEAN is_active NOT NULL DEFAULT TRUE
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    PERMISSION {
        BIGINT id PK
        VARCHAR(100) permission_name UK NOT NULL
        TEXT description
        VARCHAR(100) resource
        VARCHAR(20) action
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    ROLE_PERMISSION {
        BIGINT role_id FK
        BIGINT permission_id FK
        TIMESTAMP granted_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT granted_by
        PRIMARY KEY (role_id, permission_id)
    }

    USER_ROLE {
        BIGINT user_id FK
        BIGINT role_id FK
        DATE assigned_date NOT NULL
        DATE expiry_date
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT assigned_by
        PRIMARY KEY (user_id, role_id)
    }

    TRAINING {
        BIGINT id PK
        VARCHAR(200) training_name NOT NULL
        TEXT description
        VARCHAR(50) training_type
        INTEGER duration_hours
        DATE expiry_period_years
        BOOLEAN is_mandatory NOT NULL DEFAULT FALSE
        BOOLEAN is_active NOT NULL DEFAULT TRUE
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
    }

    USER_TRAINING {
        BIGINT id PK
        BIGINT user_id FK NOT NULL
        BIGINT training_id FK NOT NULL
        DATE completion_date
        DATE expiry_date
        VARCHAR(20) status NOT NULL
        INTEGER score
        TEXT certificate_path
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT created_by
    }

    CONFIGURATION {
        BIGINT id PK
        VARCHAR(100) config_key UK NOT NULL
        TEXT config_value NOT NULL
        VARCHAR(100) config_type
        TEXT description
        BOOLEAN is_sensitive NOT NULL DEFAULT FALSE
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT created_by
        TIMESTAMP updated_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        BIGINT updated_by
    }

    NOTIFICATION {
        BIGINT id PK
        BIGINT user_id FK
        VARCHAR(100) notification_type NOT NULL
        VARCHAR(255) title NOT NULL
        TEXT message NOT NULL
        VARCHAR(20) status NOT NULL
        TIMESTAMP created_at NOT NULL DEFAULT CURRENT_TIMESTAMP
        TIMESTAMP read_at
        TIMESTAMP sent_at
        TEXT metadata
    }
```

## Database Design Considerations

### 1. Performance Optimization
- **Indexes**: Primary keys, foreign keys, and frequently queried fields
- **Partitioning**: Large tables like TRANSACTIONS partitioned by date
- **Materialized Views**: For complex reporting queries
- **Connection Pooling**: Efficient database connection management

### 2. Data Integrity
- **Constraints**: NOT NULL, UNIQUE, CHECK constraints
- **Foreign Keys**: Referential integrity enforcement
- **Triggers**: Automated data validation and audit trail
- **Transactions**: ACID compliance for critical operations

### 3. Security
- **Encryption**: Sensitive data encrypted at rest
- **Data Masking**: For development and testing environments
- **Row Level Security**: Role-based data access
- **Audit Trail**: Complete change tracking

### 4. Scalability
- **Sharding**: For horizontal scaling of large datasets
- **Replication**: Read replicas for reporting and analytics
- **Caching**: Redis for frequently accessed data
- **Archival**: Historical data archival strategy

### 5. Indonesian Specific Features
- **KTP Validation**: Integration with DUKCAPIL
- **PPATK Integration**: Electronic filing support
- **Local Timezone**: All timestamps in WIB
- **Indonesian Language**: Support for Bahasa Indonesia
- **Regional Compliance**: Support for different regional requirements

### 6. Compliance Features
- **Data Retention**: Configurable retention policies
- **Audit Trail**: Complete activity logging
- **Data Classification**: Sensitivity labeling
- **Access Control**: Granular permissions
- **Backup and Recovery**: Regular backup strategy