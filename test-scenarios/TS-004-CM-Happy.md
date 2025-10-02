# TS-CM-004: Case Management - Happy Path Scenarios

## Test Objective
Verify successful case management workflow for suspicious activity investigations.

## Test Scenarios

### Scenario 1: Successful Case Creation from Alert
**Description**: System creates investigation case from transaction monitoring alert

**Preconditions**:
- Transaction monitoring alert exists
- Compliance officer is logged in
- Case management system is operational

**Test Steps**:
1. Compliance officer receives alert notification
2. Navigate to Alert Management Dashboard
3. Select high-priority alert:
   - Alert ID: ALT-2024-001234
   - Type: "Large Cash Transaction - Structuring Pattern"
   - Customer: Ahmad Wijaya
   - Risk Score: 4/5
   - Transactions: 3 transfers totaling Rp 270,000,000
4. Review alert details and evidence
5. Click "Create Investigation Case"
6. System populates case with alert data:
   - Case ID: INV-2024-000567
   - Priority: High
   - Status: Under Investigation
   - Assigned to: Compliance Officer
   - Due Date: 3 days from creation
7. Add investigation notes
8. Set investigation timeline
9. Case successfully created and appears in case queue

**Expected Results**:
- Case created within 2 minutes of alert selection
- All alert data transferred to case
- Case ID assigned and logged
- Priority automatically set based on alert risk
- Assignment workflow successful
- Due date calculated correctly
- Investigation timeline established
- Compliance officer notified of assignment

### Scenario 2: Successful Evidence Collection and Documentation
**Description**: System facilitates comprehensive evidence collection during investigation

**Test Steps**:
1. Open investigation case INV-2024-000567
2. Begin evidence collection process:
   - Upload transaction statements
   - Attach customer profile information
   - Add transaction monitoring logs
   - Include customer communication records
   - Upload identity verification documents
3. System organizes evidence:
   - Categorizes by evidence type
   - Timestamps all evidence uploads
   - Maintains version control
   - Generates evidence log
4. Add investigation notes and observations:
   - Transaction pattern analysis
   - Customer behavior assessment
   - Risk factor evaluation
   - Preliminary findings
5. Link related transactions and accounts
6. Evidence collection marked complete

**Expected Results**:
- All evidence properly categorized and stored
- Evidence log generated with timestamps
- Version control maintained for all documents
- Investigation notes saved and timestamped
- Related transactions linked to case
- Evidence integrity preserved
- Audit trail maintained for evidence handling
- Compliance with PPATK evidence requirements

### Scenario 3: Successful Customer Interview and Communication
**Description**: System manages customer interview process and documentation

**Test Steps**:
1. Schedule customer interview:
   - Customer: Ahmad Wijaya
   - Date/Time: Next business day
   - Method: In-person at branch office
   - Interviewer: Compliance Officer
2. System sends interview notification:
   - SMS notification to customer
   - Email confirmation with details
   - Calendar reminder for interviewer
3. Conduct interview and document responses:
   - Record customer explanation for transactions
   - Document source of funds
   - Note business purpose justification
   - Capture additional customer information
4. Upload interview documentation:
   - Signed interview form
   - Customer identification verification
   - Supporting documents provided
5. Update case with interview findings
6. Analyze interview responses for consistency

**Expected Results**:
- Interview scheduled and notifications sent
- Customer attendance confirmed
- Interview documentation complete and stored
- Responses analyzed for consistency
- Case updated with interview findings
- Documentation meets PPATK requirements
- Customer communication logged
- Interview process completed within SLA

### Scenario 4: Successful Case Analysis and Decision Making
**Description**: System supports comprehensive case analysis and decision workflow

**Test Steps**:
1. Review all collected evidence:
   - Transaction patterns and amounts
   - Customer interview responses
   - Historical customer behavior
   - Risk assessment factors
   - Regulatory threshold violations
2. Perform analysis using system tools:
   - Transaction pattern analysis
   - Customer risk assessment
   - Regulatory compliance check
   - Suspicious activity determination
3. Make investigation decision:
   - Decision: "Suspicious Activity Confirmed"
   - Reason: "Transaction structuring to avoid reporting"
   - Regulatory requirement: LTKM filing required
   - Recommendation: File LTKM with PPATK
4. Prepare decision documentation:
   - Investigation summary
   - Evidence analysis
   - Regulatory justification
   - Recommended actions
5. Submit for management approval
6. Decision workflow initiated

**Expected Results**:
- Comprehensive analysis completed
- Decision supported by evidence
- Regulatory references included
- Management approval workflow initiated
- Decision documentation complete
- Case ready for regulatory reporting
- Audit trail maintained
- SLA compliance achieved

### Scenario 5: Successful Management Approval and Case Closure
**Description**: System manages management approval and case closure process

**Test Steps**:
1. Compliance Manager reviews case:
   - Review investigation findings
   - Evaluate evidence quality
   - Assess decision justification
   - Verify regulatory compliance
2. Management decision process:
   - Approve investigation findings
   - Approve LTKM filing recommendation
   - Authorize case closure procedures
   - Set final case disposition
3. System processes approval:
   - Update case status to "Pending LTKM Filing"
   - Generate approval documentation
   - Notify compliance officer of approval
   - Initiate LTKM preparation workflow
4. Final case preparation:
   - Complete all documentation
   - Prepare for LTKM filing
   - Update customer risk profile
   - Set enhanced monitoring period
5. Case marked ready for regulatory reporting

**Expected Results**:
- Management approval completed within SLA
- Approval documentation generated
- Case status updated correctly
- Compliance team notified
- LTKM preparation initiated
- Customer risk profile updated
- Enhanced monitoring activated
- Case closure process initiated

### Scenario 6: Successful LTKM Preparation and Filing
**Description**: System prepares and files LTKM with PPATK

**Test Steps**:
1. Generate LTKM report from case data:
   - Populate PPATK LTKM format
   - Include all required sections:
     - Pelapor information
     - Customer details
     - Transaction identification
     - Transaction details
     - Reason for suspicion
     - Actions taken
2. Review and validate LTKM content:
   - Data completeness check
   - Format validation
   - Indonesian language verification
   - Regulatory compliance check
3. Submit LTKM to PPATK:
   - Electronic submission via PPATK API
   - Digital signature application
   - Submission confirmation tracking
   - Acknowledgment processing
4. Post-filing procedures:
   - Record PPATK reference number
   - Update case status to "Closed - LTKM Filed"
   - Generate filing confirmation
   - Archive case documentation

**Expected Results**:
- LTKM generated correctly in PPATK format
- All required sections complete and accurate
- Electronic submission successful
- PPATK acknowledgment received
- Reference number recorded
- Case properly closed
- Documentation archived
- Compliance achieved

## Success Criteria
- Cases created from alerts within SLA
- Evidence collection complete and properly documented
- Customer interviews scheduled and conducted
- Analysis and decision making thorough and justified
- Management approval workflow successful
- LTKM preparation and filing accurate and timely
- All actions logged and auditable
- PPATK requirements met
- Customer experience maintained professional