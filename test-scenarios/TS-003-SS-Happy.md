# TS-SS-003: Sanctions Screening - Happy Path Scenarios

## Test Objective
Verify successful sanctions and watchlist screening against domestic and international lists.

## Test Scenarios

### Scenario 1: Successful Domestic Sanctions Match (PPATK)
**Description**: System detects match against PPATK terrorist financing list

**Preconditions**:
- PPATK watchlist is updated and available
- Screening services are operational
- Customer data is available for screening

**Test Steps**:
1. New customer registration attempt:
   - Name: "Ahmad Susanto" (matches PPATK list)
   - KTP: "3205123456780001"
   - Date of Birth: "15-06-1985"
   - Address: "Bandung, Jawa Barat"
2. System performs real-time screening against PPATK list
3. Screening algorithm processes customer data
4. Exact match detected in PPATK terrorist list
5. Alert generated: "PPATK Sanctions Match - High Priority"
6. Customer registration immediately blocked
7. Enhanced verification process initiated
8. Compliance officer notified with urgency
9. PPATK reporting workflow activated
10. System creates investigation case

**Expected Results**:
- Match detected within 2 seconds
- Alert priority: Critical (5/5)
- Customer registration prevented
- Immediate compliance notification
- PPATK reporting initiated
- Investigation case auto-created
- All related accounts frozen
- System log: "PPATK match detected - action taken"

### Scenario 2: Successful PEP Detection and Enhanced Due Diligence
**Description**: System identifies Politically Exposed Person and triggers EDD

**Test Steps**:
1. Customer screening for government official:
   - Name: "Dr. Siti Nurhaliza, M.Si"
   - Position: "Direktur Jenderal, Kementerian Keuangan"
   - Institution: "Government of Indonesia"
   - KTP: "3275123456780001"
2. System screens against Indonesian PEP database
3. PEP status confirmed in government directory
4. Enhanced screening algorithm applied
5. System identifies PEP level: "Senior Government Official"
6. Enhanced due diligence automatically triggered
7. Senior management approval workflow initiated
8. Enhanced monitoring rules activated
9. Additional documentation requirements enforced
10. PEP classification: "High Risk - Enhanced Monitoring"

**Expected Results**:
- PEP detected within 3 seconds
- Risk classification: High Risk
- EDD requirements automatically applied
- Management approval workflow started
- Enhanced monitoring activated
- Quarterly screening schedule set
- All transactions subject to enhanced review
- Compliance team notified of PEP status

### Scenario 3: Successful International Sanctions Match (OFAC)
**Description**: System detects match against OFAC SDN list

**Test Steps**:
1. Corporate customer screening:
   - Company Name: "Global Trading Corporation"
   - Registration Number: "123456789"
   - Address: "Jakarta, Indonesia"
   - Directors: "John Smith" (matches OFAC list)
2. System performs multi-level screening:
   - Company name screening
   - Director name screening
   - Address screening
   - Registration number screening
3. OFAC SDN list match detected for director
4. Alert generated: "OFAC Sanctions Match - Director"
5. Enhanced company investigation initiated
6. All company accounts flagged for review
7. Transaction restrictions applied
8. Regulatory reporting prepared
9. Compliance investigation workflow activated

**Expected Results**:
- OFAC match detected within 5 seconds
- Company status: "Under Investigation"
- All transactions blocked pending review
- Enhanced due diligence for entire company
- US regulatory reporting requirements triggered
- Company risk score: Critical (5/5)
- Immediate compliance escalation

### Scenario 4: Successful Adverse Media Detection
**Description**: System detects adverse media mentions related to financial crime

**Test Steps**:
1. Customer profile screening for adverse media:
   - Customer: "PT Indo Makmur Sejahtera"
   - Directors: "Budi Santoso, Anita Wijaya"
   - Business: "Import/Export Trading"
2. System performs adverse media screening:
   - Indonesian news sources (Kompas, Tempo, Detik)
   - International financial news (Reuters, Bloomberg)
   - Regulatory enforcement databases
   - Court records and legal documents
3. Adverse media detected:
   - News article about corruption investigation
   - Court case mentioning company director
   - Regulatory enforcement action
4. Alert generated: "Adverse Media Detection - Financial Crime"
5. Enhanced investigation initiated
6. Risk assessment updated
7. Enhanced monitoring activated
8. Compliance review workflow started

**Expected Results**:
- Adverse media detected within 30 seconds
- Risk score increased to High (4/5)
- Enhanced monitoring activated
- Investigation case created with media evidence
- Customer profile updated with adverse findings
- Quarterly adverse media screening scheduled
- Compliance team notified with media links

### Scenario 5: Successful Fuzzy Matching for Name Variations
**Description**: System detects matches using fuzzy logic for name variations

**Test Steps**:
1. Customer screening with name variations:
   - Customer Name: "Muhammad Abdurrahman Al-Hadad"
   - Potential match: "Mohammed Abdul Rahman Al-Haddad"
2. System applies fuzzy matching algorithms:
   - Phonetic matching (Soundex)
   - Character similarity analysis
   - Name component comparison
   - Cultural name variation recognition
3. Fuzzy match detected with confidence score: 85%
   - Name similarity score: High
   - Additional factors verified (DOB, nationality)
   - Risk assessment based on match confidence
4. Alert generated: "Potential Sanctions Match - Fuzzy Logic"
5. Enhanced verification required
6. Manual review workflow initiated
7. Additional data collection activated

**Expected Results**:
- Fuzzy match detected within 10 seconds
- Confidence score accurately calculated
- Appropriate risk level assigned based on confidence
- Enhanced verification process initiated
- Manual review queue populated
- System learns from verification outcome
- False positive/true negative data updated

### Scenario 6: Successful Batch Screening for Existing Customers
**Description**: System performs batch screening of existing customer database

**Test Steps**:
1. Initiate batch screening process:
   - Target: All active customers (10,000+ records)
   - Purpose: Periodic rescreening requirement
   - Lists: Updated PPATK, OFAC, UN lists
2. System processes batch screening:
   - Queue management for large dataset
   - Parallel processing for efficiency
   - Progress tracking and monitoring
   - Error handling and retry logic
3. Batch processing completes:
   - 9,950 customers cleared (no matches)
   - 45 potential matches identified
   - 3 high-priority matches detected
   - 42 medium-priority matches for review
4. Results analysis and reporting:
   - Screening completion report generated
   - Match details compiled for compliance review
   - Customer risk profiles updated
   - Investigation cases created for matches

**Expected Results**:
- Batch screening completes within 1 hour
- 100% customer coverage achieved
- All matches identified and categorized
- Screening completion report generated
- Customer risk profiles updated
- Investigation cases created for matches
- Compliance dashboard updated with results
- Audit trail maintained for screening process

### Scenario 7: Successful Real-Time Transaction Screening
**Description**: System screens transactions in real-time against sanctions lists

**Test Steps**:
1. Customer initiates international transfer:
   - Sender: PT Global Traders (existing customer)
   - Beneficiary: "International Shipping Corp"
   - Amount: USD 50,000
   - Destination: High-risk jurisdiction
2. System performs real-time transaction screening:
   - Beneficiary name screening
   - Beneficiary address screening
   - Country risk assessment
   - Transaction pattern analysis
3. Beneficiary matches international sanctions list
4. Real-time alert generated: "Sanctions Match - Transaction Blocked"
5. Transaction immediately blocked
6. Compliance team notified instantly
7. Enhanced investigation initiated
8. Customer notified of transaction rejection

**Expected Results**:
- Transaction screening completed in < 1 second
- Sanctions match detected and transaction blocked
- Real-time alert to compliance team
- Customer notified immediately
- Investigation case created
- Enhanced monitoring activated for sender
- Regulatory reporting prepared
- System prevents sanctions violation

## Success Criteria
- All screening types (domestic, international, PEP, adverse media) working
- Real-time screening performance < 5 seconds
- Batch screening completes within time limits
- Fuzzy matching accuracy maintained
- Alert generation and routing working correctly
- Integration with all screening sources successful
- Compliance workflows triggered appropriately
- System maintains performance under load