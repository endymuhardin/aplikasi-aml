# FR-CM-004: Case Management System

## Requirement
The system shall implement a comprehensive case management system for investigating and documenting suspicious activities in compliance with PPATK requirements and OJK guidelines.

## Functional Requirements

### 1. Case Creation and Assignment
- **FR-CM-004.1**: System must support automated and manual case creation:
  - Automatic case generation from transaction monitoring alerts
  - Manual case creation by compliance officers
  - Case assignment based on risk level and expertise
  - Escalation procedures for high-risk cases
  - SLA tracking and deadline management

### 2. Case Investigation Workflow
- **FR-CM-004.2**: System must provide structured investigation workflow:
  - Initial assessment and risk categorization
  - Evidence collection and documentation
  - Customer interview scheduling and recording
  - Transaction analysis and pattern identification
  - Decision making and case disposition
  - Approval workflow for case closure

### 3. Evidence Management
- **FR-CM-004.3**: System must manage case evidence including:
  - Transaction records and statements
  - Customer communication records
  - Identification documents and verification results
  - External investigation reports
  - Witness statements and interview notes
  - Screen shot and transaction evidence capture

### 4. Case Status Tracking
- **FR-CM-004.4**: System must track case status throughout lifecycle:
  - New case creation
  - Under investigation
  - Pending additional information
  - Under review/approval
  - Closed (no action required)
  - Closed (SAR/STR filed)
  - Reopened for further investigation

### 5. Reporting and Documentation
- **FR-CM-004.5**: System must generate case documentation:
  - Investigation reports in Indonesian language
  - Decision justifications with regulatory references
  - Summary of findings and evidence
  - Recommendations for action
  - Regulatory filing preparation (LTKM)
  - Management summary reports

### 6. Collaboration and Communication
- **FR-CM-004.6**: System must support case collaboration:
  - Multi-user case assignment and access
  - Internal messaging and commenting
  - Document sharing and version control
  - Audit trail of all case activities
  - Notification system for case updates
  - Escalation procedures for urgent cases

### 7. Integration with PPATK Requirements
- **FR-CM-004.7**: System must comply with PPATK case management requirements:
  - Case documentation in Indonesian language
  - Mandatory fields for PPATK reporting
  - Timeline tracking for PPATK deadlines
  - Evidence collection standards
  - Interview documentation procedures
  - Regulatory filing preparation

## Case Types and Categories
### Indonesian Case Types
- **LTKM (Laporan Transaksi Keuangan Mencurigakan)**: Suspicious Transaction Reports
- **LTT (Laporan Transaksi Tunai)**: Cash Transaction Reports
- **Terrorist Financing Investigations**
- **Corruption and Bribery Cases**
- **Tax Evasion Related Cases**
- **Fraud Investigations**

### Risk-Based Categorization
- **High Priority**: Immediate PPATK filing required
- **Medium Priority**: Investigation within 30 days
- **Low Priority**: Routine investigation procedures
- **Information Only**: Documentation purposes

## Case Timeline Requirements
- **High-Risk Cases**: Investigation completion within 24 hours
- **Medium-Risk Cases**: Investigation completion within 7 days
- **Low-Risk Cases**: Investigation completion within 30 days
- **PPATK Filing**: Within 3 working days of decision
- **Documentation**: Complete case file within 5 days of closure

## Compliance References
- Peraturan OJK No. 23/POJK.01/2019 Pasal 26-30
- SE OJK No. 24/SEOJK.01/2020 tentang Tata Cara Pelaporan
- PPATK Guidelines for Case Management
- Undang-Undang Nomor 8 Tahun 2010 Pasal 23-26

## Data Retention
- Case files and documentation: Minimum 10 years
- Investigation evidence: Minimum 10 years
- Decision records: Minimum 15 years
- Audit trails: Minimum 10 years