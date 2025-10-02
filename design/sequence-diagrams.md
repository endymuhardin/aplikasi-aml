# AML Application - Sequence Diagrams

## 1. Customer Onboarding and Due Diligence Workflow

```mermaid
sequenceDiagram
    participant U as User (Compliance Officer)
    participant CC as CustomerController
    participant CS as CustomerService
    participant DS as DukcapilService
    participant SS as ScreeningService
    participant RS as RiskAssessmentService
    participant DB as Database
    participant A as AuditService

    U->>CC: POST /api/customers (CustomerDTO)
    CC->>CS: createCustomer(dto)

    CS->>DB: Save customer (initial status)
    CS->>DS: verifyKTP(customer.ktpNumber)

    DS->>DUKCAPIL API: Verify KTP
    DUKCAPIL API-->>DS: Verification result
    DS->>CS: return verification status

    CS->>SS: screenCustomer(customer)
    SS->>PPATK API: Screen against PPATK list
    PPATK API-->>SS: PPATK screening result
    SS->>OFAC API: Screen against OFAC
    OFAC API-->>SS: OFAC screening result
    SS->>PEP API: Screen against PEP database
    PEP API-->>SS: PEP screening result
    SS->>CS: return screening results

    CS->>RS: calculateRiskScore(customer, screeningResults)
    RS->>CS: return risk assessment

    CS->>DB: Update customer with risk classification
    CS->>A: logActivity("CUSTOMER_CREATED", customer)

    CS-->>CC: Customer created successfully
    CC-->>U: 201 Created + Customer details
```

## 2. Transaction Monitoring and Alert Generation

```mermaid
sequenceDiagram
    participant CB as Core Banking
    participant TC as TransactionController
    participant TMS as TransactionMonitoringService
    participant CR as ComplianceRuleEngine
    participant A as AlertService
    participant DB as Database
    participant N as NotificationService
    participant U as Compliance Officer

    CB->>TC: POST /api/transactions (TransactionData)
    TC->>TMS: analyzeTransaction(transaction)

    TMS->>CR: evaluateRules(transaction)
    CR->>DB: Load active compliance rules
    CR->>CR: Check Large Cash Transaction (≥Rp 100M)
    CR->>CR: Check Structuring Pattern
    CR->>CR: Check Geographic Risk
    CR->>CR: Check Customer Behavior
    CR-->>TMS: Rule evaluation results

    alt Alert triggered
        TMS->>A: createAlert(transaction, rule)
        A->>DB: Save alert
        A->>N: notifyComplianceTeam(alert)
        N->>U: Email/SMS notification
        A-->>TMS: Alert created
        TMS->>DB: Update transaction with alert status
    else No alert
        TMS->>DB: Save transaction (normal)
    end

    TMS-->>TC: Transaction processed
    TC-->>CB: 200 OK
```

## 3. LTKM Reporting to PPATK

```mermaid
sequenceDiagram
    participant U as Compliance Officer
    participant CC as CaseManagementController
    participant CMS as CaseManagementService
    participant RS as ReportingService
    participant PS as PpatkService
    participant PPATK as PPATK API
    participant DB as Database
    participant A as AuditService

    U->>CC: POST /api/cases/{caseId}/ltkm
    CC->>CMS: getCase(caseId)
    CMS->>DB: Load case details and evidence

    CMS->>RS: generateLTKMReport(case)
    RS->>DB: Load customer data
    RS->>DB: Load transaction data
    RS->>DB: Load investigation notes

    RS->>RS: Format LTKM in PPATK format
    Note over RS: Sections: Pelapor, Nasabah, Transaksi, Alasan Kecurigaan, Tindakan

    RS->>PS: submitToPPATK(ltkmReport)
    PS->>PPATK: POST /efiling/ltkm (signed XML)
    PPATK-->>PS: Acknowledgment with reference

    PS->>DB: Save submission record
    PS->>A: logActivity("LTKM_SUBMITTED", submission)

    PS-->>RS: PPATK reference: LTKM-2024-XXXXX
    RS->>CMS: updateCaseStatus(caseId, "LTKM_FILED")
    CMS->>DB: Update case status

    CMS-->>CC: LTKM submitted successfully
    CC-->>U: 200 OK + PPATK reference
```

## 4. Case Investigation Workflow

```mermaid
sequenceDiagram
    participant U as Compliance Officer
    participant CC as CaseManagementController
    participant CMS as CaseManagementService
    participant CS as CustomerService
    participant TS as TransactionService
    participant DB as Database
    participant N as NotificationService
    participant C as Customer

    U->>CC: GET /api/cases/{caseId}
    CC->>CMS: getCaseDetails(caseId)
    CMS->>DB: Load case with evidence

    U->>CC: POST /api/cases/{caseId}/evidence
    CC->>CMS: addEvidence(caseId, evidence)
    CMS->>DB: Save evidence documents

    U->>CC: POST /api/cases/{caseId}/interview
    CC->>CMS: scheduleInterview(caseId, dateTime)
    CMS->>N: notifyCustomer(customer, interview)
    N->>C: Interview notification

    C->>CC: Attend interview and provide information
    CC->>CMS: recordInterview(caseId, interviewNotes)
    CMS->>DB: Save interview documentation

    U->>CC: POST /api/cases/{caseId}/decision
    CC->>CMS: makeDecision(caseId, decision, justification)
    CMS->>CS: updateCustomerRisk(customerId, decision)
    CS->>DB: Update customer risk profile

    CMS->>RS: generateRequiredReports(caseId)
    alt Decision requires LTKM
        RS->>PS: submitLTKM(case)
    end

    CMS->>DB: Update case status to CLOSED
    CMS->>A: logActivity("CASE_CLOSED", case)

    CMS-->>CC: Case processed successfully
    CC-->>U: 200 OK
```

## 5. Sanctions Screening Process

```mermaid
sequenceDiagram
    participant S as Scheduled Job
    participant SS as ScreeningService
    participant WL as WatchlistService
    participant DB as Database
    participant PPATK as PPATK API
    participant OFAC as OFAC API
    participant UN as UN API
    participant A as AlertService
    participant U as Compliance Officer

    S->>SS: dailyScreeningJob()
    SS->>DB: Get customers due for screening

    loop For each customer
        SS->>WL: getActiveWatchlists()
        WL->>DB: Load PPATK, OFAC, UN, PEP lists

        SS->>PPATK: screenCustomer(customer)
        PPATK-->>SS: PPATK screening result

        SS->>OFAC: screenCustomer(customer)
        OFAC-->>SS: OFAC screening result

        SS->>UN: screenCustomer(customer)
        UN-->>SS: UN screening result

        SS->>SS: performFuzzyMatching(customer, results)

        alt Match found
            SS->>A: createScreeningAlert(customer, match)
            A->>DB: Save screening alert
            A->>U: Notify compliance officer
        end

        SS->>DB: Update screening results
    end

    SS->>A: logActivity("DAILY_SCREENING_COMPLETED")
```

## 6. User Authentication and Authorization

```mermaid
sequenceDiagram
    participant U as User
    participant AC as AuthController
    participant AS as AuthService
    participant MFA as MFAService
    participant DB as Database
    participant A as AuditService

    U->>AC: POST /api/auth/login (credentials)
    AC->>AS: authenticate(username, password)
    AS->>DB: Validate user credentials

    alt Valid credentials
        AS->>MFA: initiateMFA(user)
        MFA->>U: Send MFA challenge (SMS/App)

        U->>MFA: Provide MFA code
        MFA->>AS: validateMFA(code)

        AS->>DB: Update last login
        AS->>A: logUserLogin(user)

        AS->>AS: generateJWT(user)
        AS-->>AC: JWT token + user info
        AC-->>U: 200 OK + JWT token
    else Invalid credentials
        AS->>DB: Record failed attempt
        AS->>A: logFailedLogin(username)
        AS-->>AC: Authentication failed
        AC-->>U: 401 Unauthorized
    end
```

## 7. Audit Trail and Compliance Monitoring

```mermaid
sequenceDiagram
    participant U as User
    participant C as Any Controller
    participant S as Any Service
    participant DB as Database
    participant A as AuditService
    participant AM as AuditManager
    participant M as MonitoringService

    U->>C: Any request (e.g., update customer)
    C->>S: Process request
    S->>DB: Perform database operation

    S->>A: logActivity(action, details)
    A->>DB: Save audit log with timestamp
    A->>M: checkForSuspiciousActivity(user, action)

    alt Suspicious pattern detected
        M->>A: createSecurityAlert(user, pattern)
        A->>DB: Save security alert
        A->>AM: notifySecurityTeam(alert)
    end

    S-->>C: Operation result
    C-->>U: Response

    Note over A: Real-time audit analysis
    Note over M: Continuous monitoring for compliance
```

## 8. Integration with Core Banking System

```mermaid
sequenceDiagram
    participant CB as Core Banking
    participant GW as Gateway Service
    participant TS as TransactionService
    participant TMS as TransactionMonitoringService
    participant DB as Database
    participant ERR as ErrorHandling

    CB->>GW: Transaction data (real-time)
    GW->>TS: processTransaction(transaction)

    alt Valid transaction
        TS->>DB: Save transaction
        TS->>TMS: monitorTransaction(transaction)

        TMS->>TMS: Apply compliance rules
        TMS->>DB: Save analysis results

        alt Alert generated
            TMS->>DB: Save alert
            TMS->>CB: Notify alert
        else No alert
            TMS->>CB: Acknowledge normal processing
        end

        TS-->>GW: Processing complete
        GW-->>CB: 200 OK
    else Invalid transaction
        TS->>ERR: handleValidationError(error)
        ERR->>DB: Log error
        ERR->>CB: Error response
    end
```

These sequence diagrams cover the key workflows in the AML application, focusing on Indonesian regulatory requirements and PPATK compliance processes. Each diagram shows the interaction between components, external systems, and the flow of data through the system.