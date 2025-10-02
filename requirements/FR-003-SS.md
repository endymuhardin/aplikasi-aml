# FR-SS-003: Sanctions and Watchlist Screening

## Requirement
The system shall implement comprehensive sanctions and watchlist screening in accordance with UN Security Council resolutions, FATF recommendations, and Indonesian regulatory requirements.

## Functional Requirements

### 1. Domestic Screening (Indonesia)
- **FR-SS-003.1**: System must screen against Indonesian domestic watchlists:
  - PPATK suspected terrorists and terrorist organizations list
  - Indonesian PEP (Politically Exposed Persons) database
  - Indonesian sanctions list under UN implementation
  - Local criminal and regulatory watchlists
  - Indonesian tax evasion and fraud lists

### 2. International Sanctions Screening
- **FR-SS-003.2**: System must screen against international sanctions lists:
  - UN Security Council Consolidated List
  - OFAC (Office of Foreign Assets Control) SDN List
  - EU Consolidated Financial Sanctions List
  - UK Financial Sanctions List
  - FATF High-Risk Jurisdictions List
  - Interpol Red Notices

### 3. Politically Exposed Persons (PEP) Screening
- **FR-SS-003.3**: System must identify and screen PEPs including:
  - Indonesian government officials (national and regional)
  - Foreign government officials and diplomats
  - State-owned enterprise executives
  - Political party officials
  - Judicial and military officials
  - Family members and close associates

### 4. Adverse Media Screening
- **FR-SS-003.4**: System must perform adverse media screening:
  - Indonesian and international news sources
  - Regulatory enforcement actions
  - Corruption and fraud allegations
  - Terrorist financing investigations
  - Money laundering convictions
  - Financial crime related content

### 5. Fuzzy Matching and Logic
- **FR-SS-003.5**: System must implement intelligent matching algorithms:
  - Phonetic matching for Indonesian names
  - Fuzzy logic for spelling variations
  - Alias and alternative name matching
  - Date of birth and identification number validation
  - Geographic location correlation
  - Confidence scoring for match results

### 6. Screening Workflows
- **FR-SS-003.6**: System must support screening workflows:
  - Real-time screening for new customers
  - Periodic rescreening of existing customers
  - Transaction-level screening
  - Batch screening capabilities
  - Alert investigation and disposition
  - False positive management

### 7. Compliance with Indonesian Regulations
- **FR-SS-003.7**: System must comply with Indonesian screening requirements:
  - Mandatory screening against PPATK lists
  - PEP identification and enhanced monitoring
  - Screening frequency as per OJK guidelines
  - Documentation of screening results
  - Regulatory reporting requirements

## Screening Sources
### Indonesian Sources
- PPATK Terrorist Financing List
- Indonesian PEP Database
- KPK (Corruption Eradication Commission) lists
- Indonesian Tax Office blacklists
- Bank Indonesia regulatory lists

### International Sources
- UN Security Council Consolidated List
- OFAC SDN List
- EU Financial Sanctions List
- FATF High-Risk Countries List
- Interpol Notices
- Commercial PEP databases

## Screening Frequencies
- **New Customers**: 100% screening before onboarding
- **Existing Customers**: Annual screening
- **High-Risk Customers**: Quarterly screening
- **PEPs**: Monthly enhanced screening
- **Transactions**: Real-time for high-value transactions

## Compliance References
- Peraturan OJK No. 12/POJK.01/2017 Pasal 19-22
- UN Security Council Resolution 1373
- FATF Recommendation 6 (Sanctions)
- Undang-Undang Nomor 8 Tahun 2010 Pasal 19-22
- PPATK Regulation on Terrorist Financing

## Data Retention
- Screening results: Minimum 10 years
- Alert investigations: Minimum 10 years
- False positive records: Minimum 5 years
- Audit logs: Minimum 10 years