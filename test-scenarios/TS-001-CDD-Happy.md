# TS-CDD-001: Customer Due Diligence - Happy Path Scenarios

## Test Objective
Verify successful customer onboarding and due diligence process compliant with Indonesian regulations.

## Test Scenarios

### Scenario 1: Successful Individual Customer Onboarding
**Description**: Complete customer registration with valid Indonesian ID and documents

**Preconditions**:
- System is operational
- Compliance officer is logged in
- Customer data is valid and complete

**Test Steps**:
1. Navigate to Customer Management → New Customer
2. Enter personal information:
   - Full Name: "Ahmad Wijaya"
   - Date of Birth: "15-03-1985"
   - Place of Birth: "Jakarta"
   - KTP Number: "3175123456780001"
   - Address: "Jl. Sudirman No. 123, Jakarta Pusat"
   - Phone: "+6281234567890"
   - Email: "ahmad.wijaya@email.com"
3. Upload KTP document (valid, clear scan)
4. Upload proof of address (recent utility bill)
5. Declare source of funds: "Gaji sebagai profesional"
6. Set expected transaction volume: "Rp 50-100 juta per bulan"
7. Submit for verification
8. System performs automated risk assessment
9. Compliance officer reviews and approves
10. Customer profile is created and activated

**Expected Results**:
- Customer data is saved successfully
- KTP validation passes (DUKCAPIL integration)
- Risk score is calculated: "Medium Risk"
- Customer status: "Active"
- Compliance log is generated
- Customer receives notification
- All documents are stored in secure repository

### Scenario 2: Successful Corporate Customer Onboarding
**Description**: Complete corporate customer registration with valid business documents

**Test Steps**:
1. Navigate to Customer Management → New Corporate Customer
2. Enter business information:
   - Company Name: "PT Maju Bersama"
   - NPWP: "02.123.456.7-091.000"
   - Business Type: "Perusahaan Dagang"
   - Industry: "Retail"
   - Address: "Jl. Gatot Subroto No. 456, Jakarta Selatan"
3. Upload SIUP (Surat Izin Usaha Perdagangan)
4. Upload TDP (Tanda Daftar Perusahaan)
5. Upload company deed of establishment
6. Enter authorized person details
7. Declare business nature and expected transactions
8. Submit for compliance review
9. Enhanced due diligence is performed
10. Senior management approval obtained
11. Corporate customer is activated

**Expected Results**:
- Corporate profile created successfully
- Business documents validated
- Risk classification: "Medium-High Risk"
- EDD requirements documented
- Management approval recorded
- Customer is operational

### Scenario 3: Successful Low-Risk Customer Processing
**Description**: Process low-risk customer with standard CDD procedures

**Test Steps**:
1. Enter customer data with low-risk indicators:
   - Occupation: "Pegawai Swasta"
   - Monthly Income: "Rp 10-25 juta"
   - Expected transactions: "Rp 5-50 juta per bulan"
   - Transaction types: "Transfer biasa, pembayaran tagihan"
2. Upload standard identification documents
3. System performs automated screening:
   - No PEP matches
   - No sanctions hits
   - No adverse media
4. Risk assessment completes
5. Customer is automatically classified as "Low Risk"
6. Standard CDD procedures applied
7. Customer is activated without manual review

**Expected Results**:
- Customer classified as "Low Risk"
- Automated approval process
- Standard monitoring applied
- Compliance requirements met
- Process completion time: < 5 minutes

### Scenario 4: Successful Document Renewal Process
**Description**: Renew expired customer identification documents

**Test Steps**:
1. System detects upcoming KTP expiration (30 days before expiry)
2. Automated notification sent to customer
3. Customer uploads new KTP
4. System validates new document:
   - Format validation
   - Expiration date check
   - DUKCAPIL verification
5. Compliance officer reviews updated document
6. Document is approved
7. Customer record is updated
8. Renewal notification is logged

**Expected Results**:
- Document expiration detected and notified
- New document validated successfully
- Customer record updated
- Compliance log maintained
- Customer remains active
- Renewal process completed within SLA

## Success Criteria
- All customer data is captured accurately
- Indonesian ID validation passes
- Risk assessment completes successfully
- Documents are stored and validated
- Compliance requirements are met
- Customer is activated and operational
- Audit trail is complete and accurate