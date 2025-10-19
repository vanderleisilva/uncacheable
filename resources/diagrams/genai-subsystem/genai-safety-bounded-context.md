# GenAI Safety-First Bounded Context Diagram

This diagram visualizes the dedicated GenAI platform that MobilityCorp operates as an isolated, safety-first bounded context. It highlights the domain-specific capabilities, safety guardrails, supporting infrastructure, and compliance controls needed to deliver the intelligent customer support, safety management, incident intelligence, engagement personalization, and explainable pricing experiences promised in the architecture overview.

```mermaid
graph TD
    subgraph Clients & Operators
        CA[Customer App]
        OP[Operations Portal]
        ST[Safety Team]
        CS[Customer Support Agents]
    end

    subgraph Core Mobility Platform
        CMS[Core Mobility Services]
        IoT[Vehicle Telemetry Stream]
        CRM[CRM & Support Tickets]
        PRC[Pricing Engine]
        DWH[Data Warehouse]
    end

    CA -->|Support Queries, Booking Issues| GAAPI
    OP -->|Operational Insights| GAAPI
    ST -->|Safety Alerts, HITL Decisions| HITL
    CS -->|Escalations, Feedback| HITL

    CMS -->|Operational Events| EventBus
    IoT -->|Sensor Data| EventBus
    CRM -->|Case History| RAG
    PRC -->|Pricing Context| RAG
    DWH -->|Historical Incidents| RAG

    subgraph GenAI Safety-First Bounded Context
        GAAPI[GenAI API Gateway]
        EventBus[(Event Bus)]
        Orchestrator[GenAI Orchestrator]

        subgraph Domain Capability Pods
            CSBot[Conversational Support Agent]
            IncidentAI[Incident Intelligence Engine]
            SafetyAI[Safety Anomaly Interpreter]
            EngageAI[Engagement Personalizer]
            PricingAI[Explainable Pricing Service]
        end

        subgraph Safety Controls & Guardrails
            Policy[Policy Guardrails<br/>Prompt filtering, safety policies]
            HITL[HITL Workflow Orchestrator]
            Audit[Immutable Audit Trail]
        end

        subgraph Intelligence Assets
            RAG[RAG Grounding Layer<br/>Vector DB + Knowledge Store]
            Models[Model Serving Layer<br/>LLMs, ML models]
            Feature[Feature Store]
        end

        subgraph Assurance & Compliance
            TEVV[TEVV Pipeline<br/>Test, Evaluate, Validate, Verify]
            Monitoring[Observability & Drift Monitoring]
            Registry[Model Registry & Documentation]
            Risk[Risk & Compliance Reports]
        end

        GAAPI --> Policy --> Orchestrator
        EventBus --> Orchestrator
        Orchestrator --> CSBot
        Orchestrator --> IncidentAI
        Orchestrator --> SafetyAI
        Orchestrator --> EngageAI
        Orchestrator --> PricingAI

        CSBot --> RAG
        IncidentAI --> RAG
        SafetyAI --> RAG
        EngageAI --> Feature
        PricingAI --> RAG

        RAG --> Models
        Feature --> Models
        Models --> Policy

        CSBot --> Audit
        IncidentAI --> Audit
        SafetyAI --> Audit
        EngageAI --> Audit
        PricingAI --> Audit

        Orchestrator --> HITL
        SafetyAI --> HITL
        HITL --> Orchestrator

        Policy --> TEVV
        Models --> TEVV
        TEVV --> Registry
        Monitoring --> TEVV
        Audit --> Risk
        Registry --> Risk
        Monitoring --> Audit
    end

    Monitoring -.-> OpsFeedback[Ops Dashboards]
    OpsFeedback -.-> OP
```

The diagram emphasizes the segregation of the GenAI subsystem with layered controls: a policy-enforcing API gateway, guardrails that mediate every model interaction, rich grounding data sources, and continuous assurance pipelines that sustain EU AI Act compliance. Human oversight, observability, and immutable auditing ensure high-risk GenAI behaviors remain transparent and governable while still enabling rapid delivery of intelligent mobility experiences.
