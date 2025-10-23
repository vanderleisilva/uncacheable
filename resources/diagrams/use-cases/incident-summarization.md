# Incident Summarization

Manual incident investigations often require safety analysts to pull telemetry, support transcripts, and media from disparate tools. This slows down response times, creates inconsistent documentation, and increases the risk of missing compliance-critical details.

Incident summarization orchestrates multi-modal evidence ingestion with retrieval-augmented generation (RAG) to automatically produce a consistent timeline, root-cause clues, and recommended next actions minutes after an incident is reported.

The following evidence streams feed the summarization pipeline:

Related requirement: [REQ-AI-004 Automated incident summarization](../../../Problem-Context/requirements.md#incident-management)

- Real-time telemetry (speed, acceleration, brake events, tilt) from vehicle IoT devices
- Edge safety detections (fall detection, helmet absence, collision alerts) emitted by vision and anomaly models
- Customer and witness interactions (support transcripts, voice call recordings, chat logs)
- Photos and video attachments captured by riders, field crews, or onboard cameras
- Environmental context (weather, traffic advisories, geofence rules) to explain contributing factors

Incident summarization delivers the following outcomes:

- Generates a standardized incident brief (timeline, contributing factors, recommended mitigations) in under 10 minutes
- Flags compliance and insurance requirements with citations back to the originating evidence
- Highlights follow-up tasks for operations (vehicle recovery, customer outreach, maintenance checks)
- Feeds an incident knowledge base to surface emerging risks and inform future policy updates

## How it works

1. Telemetry, diagnostic events, and AI-triggered safety alerts stream through the **telemetry pipeline**, which normalizes and stores raw signals for downstream retrieval.
2. Media ingestion services process uploaded photos, dashcam footage, and sensor snapshots, running CV pipelines to extract labels and transcripts before archiving artifacts in an **evidence store**.
3. When an incident is opened in the **incident management service**, the **incident ingestor** collects related evidence, tags it, and publishes metadata into the **incident vector index**.
4. The **incident summarization orchestrator** performs RAG retrieval over the index, assembles a structured prompt, and calls the external LLM provider to generate a draft timeline with cited references.
5. A **validation and redaction service** verifies factual claims against the evidence set, redacts PII, stores the approved summary in the **incident reports database**, and notifies safety and compliance teams.

The following diagram illustrates the cooperation between components:

```mermaid
graph TB
    %% External Systems
    Vehicles[Fleet Vehicles<br/>IoT Sensors]
    Dashcams[Onboard Cameras]
    MobileApp[Mobile App]
    SupportChannel[Support Channels<br/><small>Chat/Voice/Email</small>]

    %% Actors
    SafetyOps[Safety Analyst<br/>Ops Dashboard]
    ComplianceOfficer[Compliance Officer<br/>Regulatory Portal]

    %% AI
    LLMProvider[LLM Provider]

    %% Streaming
    TelemetryPipeline[Telemetry Pipeline<br/>MQTT + TimescaleDB]
    MediaIngest[Media Ingestion Pipeline<br/>S3 + Vision Service]

    %% Incident Intelligence Bounded Context
    subgraph "Incident Intelligence (Bounded Context)"
        IncidentIngest[Incident Ingestor]
        EvidenceIndexer[Evidence Indexer]
        EvidenceStore[(Evidence Store)]
        VectorIndex[(Incident Vector Index)]
        Summarizer[Incident Summarization Orchestrator]
        Validator[Validation & Redaction Service]
        IncidentReports[(Incident Reports DB)]
        AuditStore[(Audit Store)]
    end

    %% Core Services
    subgraph "Core Services"
        IncidentService[Incident Management Service]
        SupportService[Support Service]
    end

    Vehicles -->|Telemetry| TelemetryPipeline
    Dashcams -->|Video & Images| MediaIngest
    MobileApp -->|Incident Report| IncidentService
    SupportChannel -->|Conversations| SupportService

    TelemetryPipeline -->|Events| IncidentIngest
    TelemetryPipeline -->|Aggregated Signals| EvidenceStore
    MediaIngest -->|Processed Media| EvidenceStore
    MediaIngest -->|Metadata| EvidenceIndexer

    SupportService -->|Escalated Transcript| IncidentService
    SupportService -->|Annotated Logs| EvidenceStore

    IncidentService -->|Create Incident| IncidentIngest
    IncidentService -->|Request Summary| Summarizer

    IncidentIngest --> |Normalize & Tag| EvidenceStore
    IncidentIngest --> VectorIndex
    TelemetryPipeline -->|Feature Embeddings| VectorIndex

    Summarizer -->|Retrieve Context| VectorIndex
    Summarizer -->|Fetch Artifacts| EvidenceStore
    Summarizer -->|Prompt| LLMProvider
    LLMProvider -->|Draft Summary| Summarizer

    Summarizer --> Validator
    Validator -->|Store Summary| IncidentReports
    Validator --> AuditStore

    IncidentReports -->|Notify| IncidentService
    IncidentService -->|Timeline & Actions| SafetyOps
    IncidentReports -->|Regulatory Package| ComplianceOfficer

    style TelemetryPipeline fill:#95A5A6
    style MediaIngest fill:#95A5A6

    style IncidentIngest fill:#4A90E2
    style EvidenceIndexer fill:#4A90E2
    style Summarizer fill:#4A90E2
    style Validator fill:#4A90E2
    style IncidentService fill:#4A90E2
    style SupportService fill:#4A90E2

    style EvidenceStore fill:#9B59B6
    style VectorIndex fill:#9B59B6
    style IncidentReports fill:#9B59B6
    style AuditStore fill:#9B59B6

    style LLMProvider fill:#E74C3C

    style SafetyOps fill:#50C878
    style ComplianceOfficer fill:#50C878
```

## References

- See [GenAI Component Diagram](../genai-subsystem/genai-component-diagram.md) for component details
- See [Incident management requirements](../../../Problem-Context/requirements.md#incident-management) for requirements details
- See [GenAI Strategy](../../../GenAI-Strategy/README.md) for conversational support use case
