# Stage 2: Payment Approval + UETR Compliance Tracking
## Detailed Process Flow - Dual Approval and Enhanced Fraud Screening

```mermaid
sequenceDiagram
    participant WorkflowEngine as ⚙️ Workflow Engine (Camunda)
    participant ComplianceEngine as 🛡️ Compliance Engine
    participant FraudDetection as 🔍 Fraud Detection Service
    participant ApprovalService as ✅ Approval Service
    participant NotificationSvc as 📧 Notification Service
    participant DataLake as 🏛️ Data Lake (Silver)
    participant KafkaEvents as 📨 Kafka Events

    Note over WorkflowEngine, KafkaEvents: 📋 STAGE 2: PAYMENT APPROVAL + UETR COMPLIANCE TRACKING
    Note right of KafkaEvents: UETR enables real-time compliance audit trail

    %% Process Step 1: Enhanced Risk Assessment with UETR
    activate WorkflowEngine
    WorkflowEngine->>ComplianceEngine: Enhanced Risk Assessment Request (UETR included)
    activate ComplianceEngine
    ComplianceEngine->>ComplianceEngine: Deep AML/KYC Analysis (UETR audit trail)
    Note right of ComplianceEngine: UETR Compliance Tracking:<br/>• Transaction Pattern Analysis<br/>• Beneficiary Risk Scoring<br/>• Geographic Risk Assessment<br/>• Currency Risk Evaluation

    %% Process Step 2: Fraud Detection Analysis with UETR
    ComplianceEngine->>FraudDetection: ML-Based Fraud Screening (UETR context)
    activate FraudDetection
    FraudDetection->>FraudDetection: Real-time ML Model Analysis (UETR-based)
    Note right of FraudDetection: UETR ML Features:<br/>• Velocity Checks (UETR history)<br/>• Behavioral Analysis<br/>• Device Fingerprinting<br/>• Transaction Clustering

    %% Process Step 3: Risk Score Calculation with UETR
    FraudDetection->>FraudDetection: Calculate Composite Risk Score (UETR indexed)
    FraudDetection-->>ComplianceEngine: Risk Score + Recommendations (UETR tracked)
    Note left of FraudDetection: UETR Risk Categories:<br/>• LOW (0-30): Auto-approve<br/>• MEDIUM (31-70): Manual review<br/>• HIGH (71-100): Block/investigate
    deactivate FraudDetection

    %% Process Step 4: Compliance Decision with UETR
    ComplianceEngine->>ComplianceEngine: Final Compliance Assessment (UETR logged)
    ComplianceEngine-->>WorkflowEngine: Compliance Decision + Risk Score (UETR audit)
    deactivate ComplianceEngine
    Note right of WorkflowEngine: ✅ UETR COMPLIANCE TARGET:<br/>Complete audit trail for regulatory reporting

    %% Process Step 5: Dual Approval Logic with UETR
    alt Risk Score: LOW (Auto-approve with UETR)
        WorkflowEngine->>WorkflowEngine: Auto-approve (UETR compliance logged)
        Note right of WorkflowEngine: UETR tracks low-risk<br/>auto-approval decision
    else Risk Score: MEDIUM/HIGH (Manual Approval with UETR)
        WorkflowEngine->>ApprovalService: Request Dual Approval (UETR reference)
        activate ApprovalService
        ApprovalService->>NotificationSvc: Send Approval Request (UETR tracking)
        activate NotificationSvc
        NotificationSvc-->>ApprovalService: Approval Notifications Sent (UETR logged)

        %% First Approval with UETR
        ApprovalService->>ApprovalService: Wait for Maker Approval #1 (UETR tracked)
        Note right of ApprovalService: UETR logs first approver decision
        ApprovalService->>ApprovalService: Wait for Maker Approval #2 (UETR tracked)
        Note right of ApprovalService: UETR logs second approver decision

        %% Final Approval Decision with UETR
        ApprovalService->>ApprovalService: Validate Dual Approval Rules (UETR audit)
        ApprovalService-->>WorkflowEngine: Dual Approval Decision (UETR completed)
        deactivate ApprovalService
        deactivate NotificationSvc
    end

    %% Process Step 6: Data Enrichment with UETR (Silver Layer)
    WorkflowEngine->>KafkaEvents: Publish Payment.Approved/Rejected Event (UETR key)
    KafkaEvents->>DataLake: Store Enriched Data (UETR-indexed Silver Layer)
    Note right of DataLake: UETR Silver Data:<br/>• Risk scores by UETR<br/>• Approval decisions<br/>• Compliance metadata<br/>• Real-time audit trail

    %% Process Step 7: Status Update with UETR
    WorkflowEngine->>WorkflowEngine: Update Payment Status (UETR tracking)
    Note right of WorkflowEngine: UETR Status Options:<br/>• APPROVED: Ready for execution<br/>• REJECTED: Send notification<br/>• PENDING: Awaiting approval
    deactivate WorkflowEngine

    Note over WorkflowEngine, KafkaEvents: 📊 UETR SILVER DATA: Complete compliance audit trail captured

```

## Stage 2 Process Steps Summary

| Step | Process | System | Target Benefit |
|------|---------|--------|----------------|
| **2.1** | Enhanced Risk Assessment | Compliance Engine | Risk Evaluation |
| **2.2** | Fraud Detection Analysis | ML Fraud Detection | ✅ **Fraud Screening** |
| **2.3** | Risk Score Calculation | Fraud Detection + Compliance | Risk Quantification |
| **2.4** | Compliance Decision | Compliance Engine | Regulatory Compliance |
| **2.5** | Dual Approval Logic | Approval Service + Workflow | Authorization Control |
| **2.6** | Data Enrichment (Silver) | Kafka + Data Lake | Audit Enhancement |
| **2.7** | Status Update | Workflow Engine | Process Control |

## Key Technical Components

### Risk Assessment Framework
- **AML/KYC Depth**: Enhanced screening beyond basic checks
- **Geographic Risk**: Country-specific risk factors
- **Transaction Patterns**: Historical behavior analysis
- **ML-Based Detection**: Real-time machine learning models

### Dual Approval Configuration
- **Auto-Approval Threshold**: Risk score 0-30
- **Manual Review Required**: Risk score 31-70
- **High-Risk Block**: Risk score 71-100
- **Maker-Checker Rule**: Minimum 2 approvers for medium/high risk

### BIAN Service Domains
- **Party Authentication**: Enhanced identity verification
- **Fraud Detection**: Primary domain for ML-based screening
- **Customer Case Management**: Approval workflow management

## Data Architecture - Silver Layer

### Enhanced Event Schema
```json
{
  "eventType": "Payment.ComplianceAssessed",
  "uetr": "DEUTDEFFXXX20241115RND123456",
  "timestamp": "2024-01-15T10:35:00Z",
  "riskAssessment": {
    "overallScore": 25,
    "category": "LOW",
    "factors": {
      "amlScore": 15,
      "fraudScore": 18,
      "geographicRisk": 10,
      "behavioralRisk": 12
    }
  },
  "approvalStatus": "AUTO_APPROVED",
  "complianceChecks": {
    "sanctionsScreen": "CLEAR",
    "pepCheck": "CLEAR",
    "fraudDetection": "LOW_RISK"
  }
}
```

## Fraud Detection Models

### ML Model Features
- **Velocity Patterns**: Transaction frequency and amounts
- **Geographic Anomalies**: Unusual destination countries
- **Behavioral Shifts**: Deviations from normal patterns
- **Network Analysis**: Relationship mapping and clustering

### Decision Matrix
| Risk Score | Action | Approval Required | Processing Time |
|------------|--------|-------------------|-----------------|
| 0-30 (LOW) | Auto-approve | None | < 1 minute |
| 31-70 (MEDIUM) | Manual review | Dual approval | 5-15 minutes |
| 71-100 (HIGH) | Block/investigate | Senior + Compliance | 30+ minutes |

## Next Stage
➡️ [Stage 3: Payment Gateway](stage3-payment-gateway.md) - Message formatting and SWIFT transmission