# FR-CDD-001: Customer Due Diligence Implementation

## Requirement
The system shall implement Customer Due Diligence (CDD) procedures in accordance with Peraturan OJK No. 12/POJK.01/2017 and Peraturan Bank Indonesia No. 14/27/PBI/2012.

## Functional Requirements

### 1. Customer Identification
- **FR-CDD-001.1**: System must collect and verify customer identification data including:
  - Full name, date of birth, place of birth
  - National ID number (KTP/SIM/Paspor)
  - Address (residential and mailing)
  - Occupation and employer information
  - Source of funds declaration
  - Expected transaction volume and frequency

### 2. Risk Assessment
- **FR-CDD-001.2**: System shall perform automated customer risk assessment based on:
  - Customer type (individual, corporate, high net worth)
  - Geographic risk factors
  - Product/service risk level
  - Transaction pattern analysis
  - PEP (Politically Exposed Person) status

### 3. Risk Classification
- **FR-CDD-001.3**: System must classify customers into risk categories:
  - Low Risk: Standard CDD procedures
  - Medium Risk: Enhanced CDD procedures
  - High Risk: Enhanced Due Diligence (EDD) with senior management approval

### 4. Document Management
- **FR-CDD-001.4**: System must store and manage customer identification documents:
  - Scanned ID documents with validity period tracking
  - Proof of address documents
  - Source of funds documentation
  - Automatic expiration notifications

### 5. Enhanced Due Diligence
- **FR-CDD-001.5**: For high-risk customers, system must implement EDD procedures:
  - Additional identity verification methods
  - Source of wealth documentation
  - Business relationship justification
  - Enhanced ongoing monitoring

## Compliance References
- Peraturan OJK No. 12/POJK.01/2017 Pasal 15-18
- Peraturan Bank Indonesia No. 14/27/PBI/2012 Pasal 8-12
- Undang-Undang Nomor 8 Tahun 2010 Pasal 11-14

## Data Retention
- Customer identification data: Minimum 5 years after relationship ends
- Risk assessment records: Minimum 10 years
- Supporting documents: Minimum 5 years