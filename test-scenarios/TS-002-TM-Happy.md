# TS-TM-002: Transaction Monitoring - Happy Path Scenarios

## Test Objective
Verify successful transaction monitoring and alert generation for suspicious activities.

## Test Scenarios

### Scenario 1: Successful Large Cash Transaction Detection
**Description**: System detects and processes cash transaction above LTT threshold

**Preconditions**:
- Customer profile exists and active
- Transaction monitoring rules are active
- Compliance monitoring dashboard is available

**Test Steps**:
1. Customer initiates cash withdrawal: Rp 150,000,000
2. System captures transaction details:
   - Amount: Rp 150,000,000
   - Type: Cash Withdrawal
   - Customer: Ahmad Wijaya (Low Risk)
   - Branch: Jakarta Pusat
   - Date/Time: Current timestamp
3. System evaluates against LTT threshold (Rp 100,000,000)
4. Alert generated: "Large Cash Transaction - LTT Reporting Required"
5. Alert routed to compliance queue
6. System creates LTT report draft
7. Compliance officer notified
8. Alert appears on monitoring dashboard
9. Transaction is logged for audit

**Expected Results**:
- Alert generated within 1 second of transaction
- Alert ID assigned and logged
- Customer profile linked to alert
- LTT report draft auto-populated
- Compliance notification sent
- Dashboard updated with real-time alert
- Risk score: Medium (3/5)
- Status: "Pending Investigation"

### Scenario 2: Successful Structuring Pattern Detection
**Description**: System detects multiple transactions designed to avoid reporting thresholds

**Test Steps**:
1. Customer performs multiple transactions in one day:
   - 09:00 - Transfer: Rp 90,000,000
   - 11:30 - Transfer: Rp 95,000,000
   - 14:15 - Transfer: Rp 85,000,000
   - Total: Rp 270,000,000
2. System monitors transaction patterns
3. Pattern recognition triggers:
   - Multiple same-day transactions
   - Each below Rp 100M threshold
   - Same beneficiary accounts
   - Structuring behavior detected
4. Alert generated: "Potential Transaction Structuring"
5. Enhanced monitoring activated
6. Compliance investigation initiated
7. All transactions flagged for review

**Expected Results**:
- Pattern detected within 5 minutes of last transaction
- Alert classification: "Suspicious Pattern"
- Risk score: High (4/5)
- All related transactions linked
- Investigation case auto-created
- Customer risk level temporarily elevated
- Real-time alert to compliance team

### Scenario 3: Successful High-Risk Geographic Transaction
**Description**: System detects transaction with high-risk geographic location

**Test Steps**:
1. Customer initiates international transfer:
   - Amount: USD 25,000
   - Destination: High-risk country (per FATF list)
   - Purpose: Business transaction
   - Customer: PT Maju Bersama (Medium Risk)
2. System checks geographic risk database
3. Cross-border rules applied
4. System evaluates against USD 10,000 threshold
5. Alert generated: "High-Risk Geographic Transaction"
6. Enhanced due diligence triggered
7. Additional documentation requested
8. Compliance review workflow initiated

**Expected Results**:
- Geographic risk alert generated immediately
- Country risk level: High
- Transaction requires enhanced documentation
- Compliance approval required before processing
- Cross-border reporting prepared
- Customer notified of additional requirements
- Risk assessment updated

### Scenario 4: Successful Unusual Transaction Pattern Detection
**Description**: System detects transactions inconsistent with customer profile

**Test Steps**:
1. Customer profile shows normal behavior:
   - Average monthly transactions: Rp 20-50 juta
   - Transaction types: Regular transfers, bill payments
   - Geographic pattern: Domestic only
2. Customer performs unusual activity:
   - Multiple international transfers
   - Large amounts (Rp 500+ juta)
   - New beneficiary countries
   - Frequency: 10+ transactions per day
3. System behavioral analysis detects anomalies
4. Pattern deviation score calculated
5. Alert generated: "Unusual Transaction Pattern"
6. Customer behavior analysis initiated
7. Compliance review triggered

**Expected Results**:
- Behavioral anomaly detected in real-time
- Deviation score: 85% (significant deviation)
- Alert priority: High
- Customer profile flagged for review
- Enhanced monitoring activated
- Investigation case created
- Historical analysis performed

### Scenario 5: Successful Rapid Fund Movement Detection
**Description**: System detects rapid movement of funds through multiple accounts

**Test Steps**:
1. Series of transactions executed:
   - Account A → Account B: Rp 200,000,000
   - Account B → Account C: Rp 195,000,000 (within 1 hour)
   - Account C → Account D: Rp 190,000,000 (within 2 hours)
   - Pattern continues through multiple accounts
2. System monitors fund flow patterns
3. Chain analysis detects layering behavior
4. Network analysis identifies related accounts
5. Alert generated: "Suspicious Fund Movement - Potential Layering"
6. Network investigation initiated
7. All related accounts flagged
8. Enhanced monitoring on entire network

**Expected Results**:
- Layering pattern detected immediately
- Network analysis completed within 5 minutes
- All related accounts identified
- Risk score: Critical (5/5)
- Immediate compliance notification
- Transaction blocking activated
- Investigation case created with network diagram
- Regulatory preparation initiated

### Scenario 6: Successful PEP Transaction Monitoring
**Description**: System properly monitors Politically Exposed Person transactions

**Test Steps**:
1. PEP customer initiates transaction:
   - Customer: Government official (PEP status)
   - Amount: Rp 75,000,000
   - Type: International transfer
   - Destination: Foreign bank account
2. System recognizes PEP status
3. Enhanced PEP monitoring rules applied
4. Transaction undergoes additional scrutiny
5. Alert generated: "PEP Transaction - Enhanced Review Required"
6. Additional compliance checks performed
7. Enhanced documentation requirements enforced

**Expected Results**:
- PEP monitoring rules automatically applied
- Enhanced risk assessment performed
- Additional compliance review required
- PEP-specific documentation requirements
- Senior management notification
- Enhanced monitoring period extended
- PEP transaction log maintained

## Success Criteria
- All suspicious patterns detected in real-time
- Alerts generated within specified timeframes
- Risk scores calculated accurately
- Compliance workflows initiated properly
- Customer profiles linked correctly
- Regulatory thresholds enforced
- Audit trails maintained
- Dashboard updated in real-time
- Notifications sent to appropriate personnel