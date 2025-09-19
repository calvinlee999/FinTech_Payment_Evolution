# Cross-Border Payment L0 Overview - 5 Stages with UETR Real-Time Tracking
## High-Level Stage Transitions with UETR-Based Payment Journey Visibility

```mermaid
sequenceDiagram
    participant Customer as 👤 Customer
    participant Frontend as 📱 Frontend Systems
    participant PaymentCore as 💰 Payment Core
    participant ComplianceLayer as 🛡️ Compliance Layer
    participant SWIFTNetwork as 🌐 SWIFT Network
    participant DataPlatform as 📊 Data Platform

    Note over Customer, DataPlatform: 🏛️ Cross-Border Payment L0 - 5-Stage Overview with UETR Tracking

    rect rgb(240, 248, 255)
        Note over Customer, PaymentCore: 🚀 STAGE 1: PAYMENT INITIATION + UETR GENERATION
        Customer->>Frontend: Initiate Payment Request
        Frontend->>PaymentCore: Create Payment + Generate UETR
        PaymentCore-->>Customer: Fee Transparency + UETR Reference
        Note right of Customer: ✅ Target: Transparency<br/>🔍 UETR: Universal Tracking ID Created
    end

    rect rgb(248, 255, 248)
        Note over PaymentCore, ComplianceLayer: 📋 STAGE 2: PAYMENT APPROVAL + UETR COMPLIANCE TRACKING
        PaymentCore->>ComplianceLayer: Dual Approval + AML Screening (with UETR)
        ComplianceLayer->>ComplianceLayer: Risk Assessment + Fraud Detection (UETR tracked)
        ComplianceLayer-->>PaymentCore: Approval Decision + UETR Status Update
        Note right of ComplianceLayer: ✅ Target: Fraud Screening<br/>🔍 UETR: Compliance Audit Trail
    end

    rect rgb(255, 248, 240)
        Note over PaymentCore, SWIFTNetwork: 🌐 STAGE 3: PAYMENT GATEWAY + UETR MESSAGE EMBEDDING
        PaymentCore->>SWIFTNetwork: Format + Send (ISO 20022/MT with UETR)
        SWIFTNetwork->>SWIFTNetwork: Message Transmission (UETR propagated)
        SWIFTNetwork-->>PaymentCore: Transmission Confirmation + UETR Receipt
        Note right of SWIFTNetwork: ✅ Target: Payment Accuracy<br/>🔍 UETR: End-to-End Message Tracking
    end

    rect rgb(255, 240, 255)
        Note over SWIFTNetwork, DataPlatform: 🔗 STAGE 4: ROUTING & EXECUTION + UETR GPI TRACKING
        SWIFTNetwork->>SWIFTNetwork: Multi-hop Routing via Correspondents (UETR tracked)
        SWIFTNetwork->>DataPlatform: gpi Status Updates with UETR (Real-time)
        DataPlatform->>DataPlatform: UETR-based Status Tracking + Retry Logic
        Note right of DataPlatform: ✅ Target: Traceability<br/>🔍 UETR: Real-Time Payment Journey Visibility
    end

    rect rgb(240, 255, 240)
        Note over DataPlatform, Customer: 📈 STAGE 5: PAYMENT INTEGRATION + UETR ANALYTICS
        DataPlatform->>DataPlatform: Update ODS + Data Lake (UETR-indexed)
        DataPlatform->>Frontend: Real-time Status Updates via UETR lookup
        Frontend-->>Customer: Completion Alerts + UETR-based tracking
        Note right of Customer: ✅ Target: Completion Alert<br/>🔍 UETR: Customer Self-Service Tracking
    end

    Note over Customer, DataPlatform: 🎯 ALL TARGET BENEFITS ACHIEVED WITH UETR END-TO-END VISIBILITY
    Note over Customer: 💎 Transparency • Traceability • Real-Time UETR Tracking
    Note over SWIFTNetwork: 🎯 Payment Accuracy • Sender Clarity • UETR-based Investigation Reduction
    Note over ComplianceLayer: 🛡️ Fraud Screening • UETR Audit Trail • Regulatory Compliance

```

## UETR-Enhanced Stage Overview Summary

| Stage | Key Systems | Primary Focus | Target Benefits | **UETR Role** |
|-------|-------------|---------------|-----------------|---------------|
| **1. Initiation** | Frontend, Payment Core | Customer Experience | 🎯 Transparency of fees & rates | **🔍 UETR Generation** - Universal identifier created |
| **2. Approval** | Compliance, Workflow | Risk Management | 🎯 Fraud Screening & Accuracy | **🔍 UETR Compliance Tracking** - Audit trail maintained |
| **3. Gateway** | Payment Formatter, SWIFT | Message Transmission | 🎯 Payment Accuracy & Sender Clarity | **🔍 UETR Message Embedding** - End-to-end tracking enabled |
| **4. Routing** | SWIFT Network, gpi | End-to-end Execution | 🎯 Traceability & Status Updates | **🔍 UETR gpi Tracking** - Real-time journey visibility |
| **5. Integration** | Data Platform, Analytics | Customer Communication | 🎯 Completion Alert & Investigation Reduction | **🔍 UETR Analytics** - Customer self-service tracking |

## Stage Transition Patterns

### Bronze → Silver → Gold Data Flow
- **Bronze (Stages 1-2)**: Raw event capture and initial validation
- **Silver (Stages 2-3)**: Enriched, validated, and formatted data
- **Gold (Stages 4-5)**: Analytics-ready data for operational dashboards

### BIAN Service Domain Alignment
- **Stage 1**: Payment Initiation Domain
- **Stage 2**: Party Authentication + Fraud Detection Domains
- **Stage 3**: Payment Execution Domain
- **Stage 4**: Payment Execution (Network) Domain
- **Stage 5**: Customer Case Management Domain

## Sub-Sequence Diagram References

For detailed process flows within each stage, refer to:
- [Stage 1: Payment Initiation](stage1-payment-initiation.md)
- [Stage 2: Payment Approval](stage2-payment-approval.md)
- [Stage 3: Payment Gateway](stage3-payment-gateway.md)
- [Stage 4: Routing & Execution](stage4-routing-execution.md)
- [Stage 5: Payment Integration](stage5-payment-integration.md)