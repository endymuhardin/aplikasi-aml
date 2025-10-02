# FR-TM-002: Transaction Monitoring System

## Requirement
The system shall implement real-time transaction monitoring to detect suspicious activities in compliance with Peraturan OJK No. 23/POJK.01/2019 and PPATK reporting requirements.

## Functional Requirements

### 1. Transaction Data Collection
- **FR-TM-002.1**: System must collect and process transaction data including:
  - Transaction amount and currency
  - Sender and receiver information
  - Transaction date and time
  - Transaction type (transfer, cash, payment, etc.)
  - Geographic location data
  - Device and channel information
  - Reference numbers and descriptions

### 2. Suspicious Pattern Detection
- **FR-TM-002.2**: System must detect suspicious patterns including:
  - Structuring transactions below reporting thresholds
  - Unusual transaction frequencies or volumes
  - Rapid movement of funds between accounts
  - Transactions with high-risk countries
  - Round number transactions
  - Transactions inconsistent with customer profile

### 3. Threshold-Based Alerts
- **FR-TM-002.3**: System must generate alerts based on regulatory thresholds:
  - Cash transactions ≥ Rp 100,000,000 (LTT reporting)
  - Cross-border transactions ≥ USD 10,000
  - Multiple transactions aggregating above thresholds
  - Transactions with sanctioned entities

### 4. Risk Scoring Engine
- **FR-TM-002.4**: System must calculate transaction risk scores based on:
  - Amount and frequency factors
  - Geographic risk assessment
  - Customer risk profile
  - Transaction type risk weighting
  - Historical behavior patterns
  - Network relationship analysis

### 5. Real-Time Monitoring
- **FR-TM-002.5**: System must provide real-time monitoring capabilities:
  - Transaction blocking for high-risk activities
  - Immediate alert generation for suspicious patterns
  - Automated escalation procedures
  - Integration with payment processing systems

### 6. Historical Analysis
- **FR-TM-002.6**: System must enable retrospective transaction analysis:
  - Transaction pattern analysis over time
  - Customer behavior monitoring
  - Trend identification and reporting
  - Historical alert management

## Alert Thresholds (Indonesian Regulations)
- **Cash Transactions**: Rp 100,000,000 (LTT threshold)
- **Cross-Border**: USD 10,000 equivalent
- **Suspicious Activity**: Any amount with suspicious indicators
- **High-Risk Countries**: Enhanced monitoring for designated countries

## Compliance References
- Peraturan OJK No. 23/POJK.01/2019 Pasal 20-25
- SE OJK No. 24/SEOJK.01/2020 tentang Transaksi Mencurigakan
- Undang-Undang Nomor 8 Tahun 2010 Pasal 15-18
- PPATK Guidelines for Transaction Monitoring

## Data Retention
- Transaction records: Minimum 5 years
- Alert records: Minimum 10 years
- Investigation documentation: Minimum 10 years