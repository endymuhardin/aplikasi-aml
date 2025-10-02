# TS-CDD-001: Customer Due Diligence - Validation and Edge Scenarios

## Test Objective
Verify system handles validation, edge cases, and error conditions in customer due diligence process.

## Validation Scenarios

### Scenario 1: Invalid KTP Number Format
**Description**: System rejects customer with invalid KTP number format

**Test Steps**:
1. Enter customer data with invalid KTP:
   - KTP Number: "12345" (too short)
   - OR KTP Number: "ABC1234567890001" (contains letters)
   - OR KTP Number: "31751234567800012" (too long)
2. Attempt to submit form
3. System validation triggers

**Expected Results**:
- Immediate error message: "Format KTP tidak valid"
- Form submission blocked
- Error message explains correct format
- Field highlighted in red
- User guidance provided

### Scenario 2: Missing Required Fields
**Description**: System validates all required fields are completed

**Test Steps**:
1. Enter partial customer data, omitting required fields:
   - Omit Date of Birth
   - Omit Address
   - Omit Phone Number
2. Attempt to proceed to next step
3. System validation occurs

**Expected Results**:
- Error message for each missing field
- Progress blocked until all required fields completed
- Clear indication of which fields are required
- User cannot advance to document upload

### Scenario 3: Document Upload Failures
**Description**: System handles various document upload issues

**Test Scenarios**:
**a) File Size Too Large**
- Upload document > 10MB
- System rejects with size limit error

**b) Invalid File Type**
- Upload .exe, .zip, or other unsupported format
- System rejects with file type error

**c) Corrupted File**
- Upload corrupted image file
- System detects and rejects file

**d) Poor Document Quality**
- Upload blurry or unclear KTP scan
- System rejects with quality error

**Expected Results**:
- Appropriate error messages for each failure type
- File validation occurs before processing
- User guidance on acceptable formats
- Progress blocked until valid document uploaded

### Scenario 4: DUKCAPIL Integration Failures
**Description**: System handles DUKCAPIL service unavailability

**Test Steps**:
1. Submit valid customer data
2. Simulate DUKCAPIL service timeout/unavailable
3. System should handle gracefully

**Expected Results**:
- User notified of temporary verification issue
- Customer data saved as "Pending Verification"
- Automatic retry mechanism initiated
- Compliance officer notified for manual review
- System logs integration failure

### Scenario 5: PEP/Sanctions Match
**Description**: System detects potential PEP or sanctions match

**Test Steps**:
1. Enter customer data matching PEP profile:
   - Name similar to known PEP
   - High-risk occupation
   - Government position
2. System performs screening
3. Potential match identified

**Expected Results**:
- Customer flagged for manual review
- Enhanced due diligence triggered
- Compliance officer alerted
- Customer status: "Under Review"
- Detailed match information provided
- Investigation workflow initiated

### Scenario 6: High-Risk Customer Processing
**Description**: System properly handles high-risk customer classification

**Test Steps**:
1. Enter customer data with high-risk indicators:
   - High transaction volume (> Rp 1 miliar per bulan)
   - High-risk occupation (Notaris, Pengacara)
   - High-risk geographic location
   - Complex business structure
2. Risk assessment identifies high risk
3. EDD requirements enforced

**Expected Results**:
- Customer classified as "High Risk"
- Enhanced due diligence required
- Senior management approval workflow
- Additional documentation required
- Enhanced monitoring rules applied
- Compliance officer approval mandatory

### Scenario 7: Duplicate Customer Detection
**Description**: System prevents duplicate customer creation

**Test Steps**:
1. Attempt to register customer with existing KTP number
2. System checks for duplicates
3. Potential duplicate detected

**Expected Results**:
- Warning message about potential duplicate
- Existing customer information displayed
- Option to update existing customer vs. create new
- Compliance officer notification for review
- Duplicate prevention log maintained

### Scenario 8: Data Validation Errors
**Description**: System validates various data field formats

**Test Scenarios**:
**a) Invalid Email Format**
- Enter: "invalid-email"
- Expected: "Format email tidak valid"

**b) Invalid Phone Number**
- Enter: "12345" (incomplete)
- Expected: "Nomor telepon tidak valid"

**c) Invalid Date Format**
- Enter: "32/13/2023" (invalid date)
- Expected: "Format tanggal tidak valid"

**d) Invalid Postal Code**
- Enter: "ABCDE" (letters instead of numbers)
- Expected: "Kode pos harus berupa angka"

**Expected Results**:
- Real-time validation feedback
- Clear error messages in Indonesian
- Field-specific error indicators
- Form submission blocked until valid

### Scenario 9: Age Validation
**Description**: System validates customer meets minimum age requirements

**Test Steps**:
1. Enter customer data with age < 17 years
2. Attempt to submit registration
3. System validates age

**Expected Results**:
- Error message: "Usia minimum 17 tahun"
- Registration blocked
- Parent/guardian information required if minor
- Compliance officer notified

### Scenario 10: Network Timeout During Submission
**Description**: System handles network issues during submission

**Test Steps**:
1. Complete customer registration form
2. Submit during simulated network timeout
3. System handles timeout gracefully

**Expected Results**:
- User notified of technical difficulties
- Data saved locally if possible
- Retry option provided
- No data loss occurs
- Error logged for technical support

## Edge Cases
### Scenario 11: Customer with Multiple Nationalities
**Description**: System handles customers with multiple citizenships

**Test Steps**:
1. Register customer with Indonesian + foreign citizenship
2. Upload multiple passports
3. System processes multiple nationalities

**Expected Results**:
- Both nationalities recorded
- Enhanced risk assessment for foreign ties
- Additional documentation requirements
- Proper risk classification applied

### Scenario 12: Customer Name with Special Characters
**Description**: System validates names with Indonesian special characters

**Test Steps**:
1. Enter name with special characters: "Muhammad Abdurrahman al-Hadad"
2. System processes special characters

**Expected Results**:
- Special characters accepted and stored correctly
- Name displays properly in all interfaces
- Search functions work with special characters
- Reports display names correctly

## Error Handling Requirements
- All error messages in Indonesian language
- Clear, actionable error guidance
- No data loss during validation failures
- Comprehensive error logging
- User-friendly error recovery options