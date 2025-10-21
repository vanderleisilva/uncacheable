# Sequence Diagram - Safety Anomaly Detection with HITL

## Description

This sequence diagram shows how the GenAI Platform detects and explains safety anomalies in real-time, with mandatory Human-in-the-Loop (HITL) approval for high-risk actions like vehicle immobilization. This satisfies EU AI Act requirements for high-risk AI systems.

## Use Case

A vehicle exhibits dangerous behavior (rapid battery depletion, erratic movement, potential theft). The system detects the anomaly, generates a human-readable explanation, and requires human approval before taking safety-critical actions.

## Example Anomaly

Vehicle #7823 (eBike) shows abnormal movement pattern at 11:30 PM in low-activity zone, with GPS spoofing indicators. System recommends immobilization to prevent theft.

## Actors & Systems

- **Vehicle**: eBike reporting suspicious telemetry
- **Telemetry Pipeline**: Real-time sensor monitoring
- **Anomaly Detector**: ML-based anomaly detection
- **GenAI Platform**: Explains anomaly and recommends actions
- **HITL Gateway**: Routes high-risk decisions to humans
- **Ops Team**: Human operators with safety decision authority
- **Fleet Service**: Executes vehicle commands
- **Audit Store**: Complete compliance logging

## Diagram

```mermaid
sequenceDiagram
    actor Vehicle as Vehicle #7823<br/>(eBike)
    participant TelemetryService as Telemetry Pipeline
    participant AnomalyDetector as Anomaly Detector<br/>(ML Model)
    participant EventBus as Event Bus
    participant GenAI as GenAI Platform
    participant RAG as RAG Retriever
    participant LLM as External LLM
    participant RiskAssessor as Risk Assessor
    participant HITL as HITL Gateway
    participant ApprovalQueue as Approval Queue
    actor OpsTeam as Operations Team
    participant FleetService as Fleet Service
    participant AuditStore as Audit Store

    Note over Vehicle: Suspicious activity at 23:30
    Vehicle->>TelemetryService: Stream telemetry:<br/>{gps: [jumping coords],<br/>speed: 45 km/h,<br/>battery: 42% (rapid drain),<br/>lock_status: unlocked,<br/>time: 23:30}

    TelemetryService->>AnomalyDetector: Real-time analysis

    Note over AnomalyDetector: ML Model Scoring
    AnomalyDetector->>AnomalyDetector: Detect anomalies:<br/>• GPS spoofing (conf: 0.89)<br/>• Unusual time/location (conf: 0.78)<br/>• Rapid battery drain (conf: 0.71)<br/>• Theft pattern (conf: 0.82)

    AnomalyDetector->>AnomalyDetector: Aggregate risk score: 0.85<br/>(HIGH RISK)

    Note over AnomalyDetector,EventBus: Publish Critical Event
    AnomalyDetector->>EventBus: Publish:<br/>safety.anomaly.critical<br/>{vehicleId: 7823,<br/>anomalies: [...],<br/>risk_score: 0.85,<br/>severity: HIGH}

    EventBus->>GenAI: Subscribe: safety.anomaly.critical

    Note over GenAI: Generate Human-Readable Explanation
    GenAI->>RAG: Retrieve context:<br/>- Similar theft patterns<br/>- Vehicle history<br/>- Location risk data
    RAG-->>GenAI: Context assembled:<br/>5 similar theft attempts<br/>in this zone

    GenAI->>LLM: Generate explanation:<br/>"Explain this safety anomaly<br/>with evidence and recommendations"

    LLM-->>GenAI: Natural language explanation:<br/>"Vehicle shows GPS spoofing...<br/>consistent with theft attempt...<br/>recommend immediate immobilization"

    Note over GenAI,RiskAssessor: Assess Risk Level
    GenAI->>RiskAssessor: Evaluate recommended action:<br/>ACTION: Immobilize vehicle

    RiskAssessor->>RiskAssessor: Check action risk matrix:<br/>• Immobilization = HIGH RISK<br/>• Safety critical = TRUE<br/>• Requires HITL = TRUE

    RiskAssessor-->>GenAI: Risk level: HIGH<br/>HITL Required: YES

    Note over GenAI,HITL: Route to Human Approval
    GenAI->>HITL: Create HITL request:<br/>{<br/> vehicleId: 7823,<br/> anomaly_explanation: "...",<br/> recommended_action: "immobilize",<br/> evidence: [...],<br/> risk_score: 0.85,<br/> confidence: 0.91<br/>}

    HITL->>ApprovalQueue: Queue for human review<br/>Priority: HIGH
    ApprovalQueue->>ApprovalQueue: Assign to available operator<br/>SLA: 5 minutes

    Note over ApprovalQueue,OpsTeam: Human Decision Required
    ApprovalQueue->>OpsTeam: Push notification + dashboard alert:<br/>"HIGH RISK: Vehicle #7823<br/>potential theft - review required"

    OpsTeam->>OpsTeam: Review AI explanation:<br/>• GPS anomaly evidence<br/>• Similar past incidents<br/>• Real-time telemetry<br/>• Vehicle location on map

    alt Human Approves Action
        OpsTeam->>HITL: APPROVE immobilization<br/>{<br/> approved_by: "operator_jane_doe",<br/> notes: "Clear theft pattern,<br/> customer not responding",<br/> timestamp: 23:33:12<br/>}

        Note over HITL: Approval granted in 2.5 minutes
        HITL->>GenAI: Approval received

        Note over GenAI,FleetService: Execute Approved Action
        GenAI->>FleetService: POST /vehicles/7823/immobilize<br/>{reason: "theft_prevention",<br/>approval_id: "approval_xyz",<br/>operator: "jane_doe"}

        FleetService->>Vehicle: Send IMMOBILIZE command<br/>(MQTT)
        Vehicle->>Vehicle: Engage electronic lock<br/>Disable motor
        Vehicle-->>FleetService: ACK: Immobilized successfully
        FleetService-->>GenAI: Immobilization confirmed

        GenAI->>EventBus: Publish:<br/>vehicle.immobilized<br/>{reason, approval_id}

    else Human Rejects Action
        OpsTeam->>HITL: REJECT immobilization<br/>{<br/> rejected_by: "operator_john_smith",<br/> reason: "Customer just called,<br/> legitimate use in area",<br/> alternative_action: "monitor_only"<br/>}

        HITL->>GenAI: Rejection received
        GenAI->>FleetService: POST /vehicles/7823/monitor<br/>{enhanced_tracking: true}

    else Human Requests More Info
        OpsTeam->>HITL: REQUEST_INFO<br/>"Check if customer reported<br/>vehicle as stolen"

        HITL->>GenAI: Additional context needed
        GenAI->>GenAI: Query customer support DB
        GenAI-->>HITL: No theft reports filed
        HITL-->>OpsTeam: Updated context provided

        Note over OpsTeam: Ops team makes decision with<br/>additional information
    end

    Note over GenAI,AuditStore: Complete Audit Trail
    GenAI->>AuditStore: Store complete record:<br/>{<br/> anomaly_detected: [timestamp],<br/> ai_explanation: "...",<br/> evidence: [...],<br/> recommended_action: "immobilize",<br/> ai_confidence: 0.91,<br/> hitl_request_time: 23:31:15,<br/> human_decision: "APPROVED",<br/> human_operator: "jane_doe",<br/> human_decision_time: 23:33:40,<br/> decision_rationale: "...",<br/> action_executed: "immobilize",<br/> action_confirmed: 23:33:45,<br/> total_response_time: 2min 30sec<br/>}

    AuditStore-->>GenAI: Audit ID: aud_safety_001

    Note over OpsTeam: Alert customer & create incident
    OpsTeam->>OpsTeam: Contact customer:<br/>"We secured your vehicle<br/>due to suspicious activity"
```

## Risk Assessment Matrix

| Action Type        | Risk Level | HITL Required | Max Auto Confidence |
| ------------------ | ---------- | ------------- | ------------------- |
| Monitor vehicle    | LOW        | No            | N/A                 |
| Alert ops team     | LOW        | No            | N/A                 |
| Notify customer    | LOW        | No            | N/A                 |
| Restrict speed     | MEDIUM     | No            | >95%                |
| Lock vehicle       | HIGH       | **YES**       | Never auto          |
| Immobilize vehicle | HIGH       | **YES**       | Never auto          |
| Remote shutdown    | CRITICAL   | **YES**       | Never auto          |

## HITL Request Format

```json
{
  "hitl_request_id": "hitl_20250315_001",
  "priority": "HIGH",
  "vehicle_id": "7823",
  "vehicle_type": "ebike",
  "timestamp_detected": "2025-03-15T23:31:15Z",
  "sla_deadline": "2025-03-15T23:36:15Z",

  "anomaly_explanation": {
    "summary": "Vehicle #7823 exhibits multiple indicators consistent with theft attempt: GPS coordinate jumping suggests spoofing device, movement in low-activity zone at unusual hour (23:30), and rapid battery depletion pattern.",
    "confidence": 0.91,
    "evidence": [
      {
        "type": "gps_anomaly",
        "description": "GPS coordinates jumping 200m every 10 seconds",
        "confidence": 0.89,
        "source": "telemetry_stream"
      },
      {
        "type": "location_risk",
        "description": "Movement in area with 12 theft incidents in last 30 days",
        "confidence": 0.78,
        "source": "historical_incidents"
      },
      {
        "type": "behavioral_pattern",
        "description": "Pattern matches 5 previous confirmed theft attempts",
        "confidence": 0.82,
        "source": "ml_classifier"
      }
    ]
  },

  "recommended_action": {
    "action": "immobilize_vehicle",
    "risk_level": "HIGH",
    "rationale": "Preventing potential theft outweighs temporary customer inconvenience. Customer can verify identity and unlock via app.",
    "alternative_actions": ["monitor_and_alert", "restrict_speed_to_5kmh"]
  },

  "context": {
    "customer_id": "cust_5234",
    "customer_contact": "+1-555-0123",
    "trip_status": "in_progress",
    "trip_start_time": "2025-03-15T23:15:00Z",
    "location": {
      "lat": 52.52,
      "lon": 13.405,
      "area": "Berlin Neukölln",
      "risk_level": "HIGH"
    },
    "vehicle_history": {
      "total_trips": 847,
      "last_maintenance": "2025-03-10",
      "previous_incidents": 0
    }
  },

  "ai_metadata": {
    "model_version": "anomaly-detector-v2.1",
    "similar_incidents_retrieved": 5,
    "rag_sources": ["incident_db", "location_risk_db", "theft_patterns"]
  }
}
```

## HITL Dashboard Features

### Real-time Information

- Live telemetry stream
- Vehicle location on map
- GPS trace visualization
- Battery/speed graphs

### Decision Support

- AI explanation in plain language
- Similar past incidents with outcomes
- Customer profile and trip history
- Risk assessment breakdown

### Action Options

- ✅ **Approve** - Execute recommended action
- ❌ **Reject** - Override AI recommendation
- ⏸️ **Request More Info** - Query additional data
- 🔄 **Alternative Action** - Specify different response

### Communication

- One-click customer contact
- Auto-generated SMS templates
- Incident report creation
- Police report integration (if needed)

## Performance Metrics

- **HITL Response Time**: 2.5 minutes average (SLA: 5 min)
- **Approval Rate**: 73% of AI recommendations approved
- **False Positive Rate**: 8.3% (AI flagged, human determined safe)
- **Prevented Thefts**: 47 confirmed in 6 months
- **Customer Satisfaction**: 4.1/5 (even when immobilized)

## EU AI Act Compliance

### High-Risk System Classification

✅ Safety-critical vehicle control  
✅ Property protection (theft prevention)

### Required Controls (All Implemented)

- ✅ **Human Oversight**: HITL gateway for high-risk actions
- ✅ **Risk Management**: Risk assessment matrix
- ✅ **Transparency**: Plain-language explanations
- ✅ **Accuracy**: 91.7% accuracy on historical data
- ✅ **Record-Keeping**: Complete audit trails
- ✅ **Cybersecurity**: Secure command channels

## Error Handling

### No Human Available (SLA Breach)

- Escalate to senior ops team
- Send alerts via multiple channels (SMS, call, email)
- If still no response after 10 min: conservative default (monitor only, no action)

### Communication Failure with Vehicle

- Retry command 3 times
- If fails: log as "action_attempted_unconfirmed"
- Dispatch field technician if critical

### Customer Dispute

- All decisions reversible via ops dashboard
- Audit trail provided as evidence
- Compensation process for false positives

## Security Considerations

- **Command Authentication**: Multi-factor auth for immobilization commands
- **Anti-Spoofing**: Vehicle commands signed with rolling codes
- **Audit Integrity**: Immutable logs with cryptographic hashing
- **Access Control**: HITL operators require special certification

## References

- See [GenAI Component Diagram](../genai-subsystem/genai-component-diagram.md) for HITL Gateway details
- See [EU AI Act Compliance](../../../AI-Governance-Compliance/eu-ai-act-compliance.md)
- See [Safety Anomaly Use Case](../../../GenAI-Strategy/use-cases.md#safety-anomaly-explanation)
