# FR-RR-005: Regulatory Reporting Requirements

## Requirement
The system shall implement automated regulatory reporting to PPATK (Pusat Pelaporan dan Analisis Transaksi Keuangan) and other Indonesian regulatory authorities in compliance with applicable laws and regulations.

## Functional Requirements

### 1. LTKM (Laporan Transaksi Keuangan Mencurigakan) Reporting
- **FR-RR-005.1**: System must generate LTKM reports for PPATK including:
  - Complete customer identification information
  - Detailed transaction description and analysis
  - Reason for suspicion in Indonesian language
  - Transaction amount and currency details
  - Involved parties and their relationships
  - Supporting evidence and documentation
  - Reporter information and certification

### 2. LTT (Laporan Transaksi Tunai) Reporting
- **FR-RR-005.2**: System must generate LTT reports for cash transactions:
  - Cash transactions ≥ Rp 100,000,000
  - Customer identification and transaction details
  - Transaction purpose and business justification
  - Source of funds information
  - Multiple transaction aggregation reporting
  - Automated threshold detection and reporting

### 3. PPATK Electronic Filing Integration
- **FR-RR-005.3**: System must integrate with PPATK electronic filing system:
  - Direct API integration with PPATK reporting portal
  - XML/JSON format compliance with PPATK specifications
  - Digital signature requirements for submissions
  - Acknowledgment receipt processing
  - Error handling and resubmission capabilities
  - Submission status tracking and notifications

### 4. OJK Compliance Reporting
- **FR-RR-005.4**: System must generate OJK compliance reports:
  - Monthly AML program effectiveness reports
  - Quarterly risk assessment summaries
  - Annual compliance certification
  - Suspicious activity statistics
  - Staff training and competency reports
  - System performance and monitoring metrics

### 5. Bank Indonesia Reporting
- **FR-RR-005.5**: System must support Bank Indonesia reporting requirements:
  - Foreign transaction reporting
  - Large transaction monitoring reports
  - Cross-border transaction summaries
  - Currency transaction reports
  - Compliance with PBI regulations

### 6. Report Generation and Validation
- **FR-RR-005.6**: System must provide report generation capabilities:
  - Automated report population from case data
  - Data validation and completeness checks
  - Format compliance with regulatory templates
  - Pre-submission quality assurance
  - Audit trail for report modifications
  - Version control and document management

### 7. Timeline Management
- **FR-RR-005.7**: System must manage regulatory reporting timelines:
  - LTKM filing within 3 working days of detection
  - LTT filing within 14 working days of transaction
  - Monthly OJK reports by 10th of following month
  - Quarterly reports within 30 days of quarter end
  - Annual reports within 90 days of year end
  - Deadline monitoring and escalation procedures

## Report Format Requirements

### LTKM Report Components
- **Section A**: Pelapor (Reporter) Information
- **Section B**: Nasabah/Rekanan (Customer/Partner) Information
- **Section C**: Identitas Transaksi (Transaction Identification)
- **Section D**: Keterangan Transaksi (Transaction Details)
- **Section E**: Alasan Kecurigaan (Reason for Suspicion)
- **Section F**: Tindakan yang Diambil (Actions Taken)

### LTT Report Components
- **Section A**: Pelapor Information
- **Section B**: Nasabah Information
- **Section C**: Transaksi Tunai Details
- **Section D**: Tujuan Transaksi (Transaction Purpose)
- **Section E**: Sumber Dana (Source of Funds)

## Integration Requirements
- **PPATK API**: Direct integration with PPATK electronic reporting system
- **Digital Signature**: Integration with Indonesian digital certificate providers
- **Secure Communication**: Encrypted data transmission to regulatory authorities
- **Acknowledgment Processing**: Automated receipt and confirmation handling

## Compliance References
- Undang-Undang Nomor 8 Tahun 2010 Pasal 27-30
- Peraturan PPATK No. 3 Tahun 2011 tentang Tata Cara Pelaporan
- Peraturan OJK No. 23/POJK.01/2019 Pasal 31-35
- SE OJK No. 24/SEOJK.01/2020 tentang Format Pelaporan
- Peraturan Bank Indonesia No. 14/27/PBI/2012 Pasal 25-28

## Data Retention
- Submitted reports: Minimum 10 years
- Report drafts and versions: Minimum 5 years
- Acknowledgment receipts: Minimum 10 years
- Supporting documentation: Minimum 10 years
- Audit trails: Minimum 10 years