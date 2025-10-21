# MobilityCorp - AI-Enabled Vehicle-Sharing Platform

> **O'Reilly Architecture Kata 2025** - An intelligent, scalable vehicle-sharing platform powered by GenAI for enhanced operations, safety, and customer experience.

## Executive Summary

MobilityCorp operates a multi-modal vehicle-sharing platform supporting **electric scooters, eBikes, electric cars, and vans** across urban environments. Our architecture addresses the core challenges of fleet operations, real-time safety, and customer support through an **AI-first approach** while maintaining strict compliance with EU AI Act regulations.

### The Challenge

Traditional vehicle-sharing platforms struggle with:

- **Fleet Distribution**: Right vehicles aren't in the right places at the right times
- **Demand Anticipation**: Unable to predict and proactively position fleet for customer needs
- **Battery Management**: Vehicles running out of charge, inefficient battery swap prioritization, no charge-sufficiency checks before bookings
- **Customer Reliability**: Ad-hoc usage patterns prevent building trust for regular commutes
- **Operational Costs**: High costs for customer support and incident management
- **Slow Response**: Delayed response times for safety anomalies and fleet incidents
- **AI Uncertainty**: Dealing with rapid AI model changes, price fluctuations, and provider reliability risks
- **AI Validation**: Ensuring AI functionality works correctly and detecting when AI starts misbehaving in production
- **AI Compliance**: Complex regulatory requirements for AI in safety-critical systems

### Our Solution: GenAI as a Safety-First Bounded Context

MobilityCorp delivers an **AI-augmented operations platform** that reduces costs while maintaining safety through:

**Fleet Intelligence:**

- **Demand Forecasting**: ML-powered prediction of demand by location, time, and events to position vehicles proactively
- **Rebalancing Optimization**: AI-driven route planning for fleet crews to maximize vehicle availability
- **Battery Intelligence**: Predictive charge modeling to prevent charge-outs, optimize battery swap priorities, and block bookings with insufficient charge
- **Pre-Positioning**: Anticipatory vehicle placement for regular commuters to build service reliability

**Operations & Safety:**

- **Intelligent Customer Support**: AI-powered conversational assistant handles 40% of support queries with RAG-grounded responses
- **Proactive Safety Management**: Real-time anomaly detection with natural language explanations and HITL gates
- **Automated Incident Intelligence**: 10x faster incident investigation through AI-generated summaries

**AI Quality & Governance:**

- **TEVV Pipeline**: Continuous Test, Evaluate, Validate, Verify process to detect AI misbehavior and ensure quality
- **Model Monitoring**: Real-time drift detection, hallucination tracking, and performance degradation alerts
- **Provider Resilience**: Abstraction layer for LLM providers, shadow mode testing, and graceful degradation strategies
- **Compliance by Design**: EU AI Act compliance with immutable audit trails, model registry, and human oversight

**Customer Experience:**

- **Personalized Engagement**: Tailored recommendations based on individual usage patterns to increase retention
- **Transparent Pricing**: Natural language explanations for dynamic pricing to build customer trust

**Architectural Differentiator**: Our GenAI Service operates as an **isolated, observable subsystem** with built-in safeguards—RAG grounding prevents hallucinations, TEVV pipeline ensures quality, immutable audit trails provide compliance, and HITL gates enforce human oversight for safety-critical decisions. This bounded context approach allows us to innovate rapidly with AI while maintaining EU AI Act compliance for high-risk vehicle operations.

## Quick Navigation

### 📋 Problem & Requirements

- [Problem Context](Problem-Context/) - Business case, actors, and constraints
  - [Business Case](Problem-Context/business-case.md)
  - [Requirements](Problem-Context/requirements.md)
  - [Actors & Personas](Problem-Context/actors-and-personas.md)
  - [Constraints](Problem-Context/constraints.md)
  - [Assumptions](Problem-Context/assumptions.md)

### 🤖 GenAI Strategy (Our Differentiator)

- [GenAI Strategy](GenAI-Strategy/) - **START HERE for innovation**
  - [Use Cases](GenAI-Strategy/use-cases.md) - Conversational support, incident summarization, anomaly detection
  - [Value Proposition](GenAI-Strategy/value-proposition.md) - Why GenAI is the competitive advantage
  - [Architecture Integration](GenAI-Strategy/architecture-integration.md) - How GenAI fits in the system
  - [AI Risk Classification](GenAI-Strategy/ai-risk-classification.md) - EU AI Act assessment

### ✅ GenAI Verification & Validation

- [GenAI Verification & Validation](GenAI-Verification-Validation/) - **Quality assurance**
  - [TEVV Overview](GenAI-Verification-Validation/tevv-overview.md) - Test, Evaluate, Validate, Verify
  - [Testing Strategy](GenAI-Verification-Validation/testing-strategy.md) - Unit, integration, adversarial
  - [Acceptance Criteria](GenAI-Verification-Validation/acceptance-criteria.md) - Concrete thresholds
  - [Monitoring Strategy](GenAI-Verification-Validation/monitoring-strategy.md) - Drift, hallucination, metrics
  - [Continuous Validation](GenAI-Verification-Validation/continuous-validation.md) - Feedback loops
  - [TEVV Pipeline Diagram](resources/diagrams/tevv-pipeline/tevv-pipeline-flow.md) ⭐

### ⚖️ AI Governance & Compliance

- [AI Governance & Compliance](AI-Governance-Compliance/) - **EU AI Act compliance**
  - [EU AI Act Compliance](AI-Governance-Compliance/eu-ai-act-compliance.md) ⭐
  - [Model Registry Strategy](AI-Governance-Compliance/model-registry-strategy.md)
  - [Audit Trail Design](AI-Governance-Compliance/audit-trail-design.md)
  - [Model Cards](AI-Governance-Compliance/model-cards/)
    - [Conversational Support Model](AI-Governance-Compliance/model-cards/conversational-support-model.md)
    - [Incident Classifier Model](AI-Governance-Compliance/model-cards/incident-classifier-model.md)
    - [Safety Anomaly Detector](AI-Governance-Compliance/model-cards/safety-anomaly-detector.md)
  - [Privacy & Security](AI-Governance-Compliance/privacy-security.md)

### 💾 Data Architecture

- [Data Architecture](Data-Architecture/)
  - [Data Model](Data-Architecture/data-model.md) - Core domain entities
  - [RAG Index Strategy](Data-Architecture/rag-index-strategy.md) ⭐
  - [Data Provenance](Data-Architecture/data-provenance.md) - Source tracking
  - [CRUD Matrix](Data-Architecture/crud-matrix.md) - Service data ownership
  - [RAG Data Flow Diagram](resources/diagrams/data-flow/rag-data-flow.md) ⭐

### 🎯 Quality Attributes

- [Quality Attributes](Quality-Attributes/) - How we achieve quality goals
  - [Scalability](Quality-Attributes/scalability.md)
  - [Availability](Quality-Attributes/availability.md)
  - [Security](Quality-Attributes/security.md)
  - [AI Safety](Quality-Attributes/ai-safety.md) ⭐
  - [Explainability](Quality-Attributes/explainability.md) ⭐
  - [Cost Analysis](Quality-Attributes/cost-analysis.md)

### ⚠️ Risks & Tradeoffs

- [Risks & Tradeoffs](Risks-Tradeoffs/)
  - [Technical Risks](Risks-Tradeoffs/technical-risks.md) - Hallucination, drift, latency
  - [Architectural Tradeoffs](Risks-Tradeoffs/architectural-tradeoffs.md) - Pros & cons
  - [AI-Specific Risks](Risks-Tradeoffs/ai-specific-risks.md) - Prompt injection, bias
  - [Mitigation Strategies](Risks-Tradeoffs/mitigation-strategies.md)

## Architecture Overview

### 📝 Architecture Decision Records

- [Architecture Decision Records](Architecture-Decision-Records/) - **Critical decisions & rationale**
  - [ADR Template](Architecture-Decision-Records/000-adr-template.md) - Standard format for new ADRs
  - [ADR-001: Microservices Architecture](Architecture-Decision-Records/001-microservices-architecture.md)
  - [ADR-002: Event-Driven Backbone](Architecture-Decision-Records/002-event-driven-backbone.md)
  - [ADR-003: Core Services Architecture](Architecture-Decision-Records/003-core-services-container-diagram.md)

### 🎨 Architecture Views & Diagrams

- [Architecture Views](Architecture-Views/) - **Visual documentation**
  - [Context Diagram](resources/diagrams/context/context-diagram.md) - System boundary
  - [Container Diagram](resources/diagrams/container/container-diagram.md) - High-level components
  - [GenAI Component Diagram](resources/diagrams/genai-subsystem/genai-component-diagram.md) ⭐
  - [Deployment Diagram](resources/diagrams/deployment/deployment-diagram.md) - Infrastructure
  - [Sequence Diagrams](resources/diagrams/sequence/) - Key flows
    - [Conversational Support](resources/diagrams/sequence/conversational-support-flow.md) ⭐
    - [Incident Summarization](resources/diagrams/sequence/incident-summarization-flow.md) ⭐
    - [Safety Anomaly Detection](resources/diagrams/sequence/safety-anomaly-detection-flow.md) ⭐
    - [Vehicle Booking](resources/diagrams/sequence/vehicle-booking-flow.md)

### GenAI Service Architecture

The GenAI Service is our key differentiator, implementing responsible AI with safety controls:

**See:** [GenAI Component Diagram](resources/diagrams/genai-subsystem/genai-component-diagram.md) for detailed view

## GenAI Value Proposition

### Operations & Support

| Use Case                     | Business Value                                         | Technical Approach                                                      | Metrics                                            |
| ---------------------------- | ------------------------------------------------------ | ----------------------------------------------------------------------- | -------------------------------------------------- |
| **Conversational Support**   | 40% ops load reduction<br/>Significant annual savings  | RAG + LLM with citations<br/>Confidence threshold: 90%                  | Factuality: 96.2%<br/>User satisfaction: 4.3/5     |
| **Incident Summarization**   | 10x faster investigation<br/>Consistent documentation  | RAG over historical incidents<br/>Automated report generation           | Report gen time: 8.2s<br/>Accuracy: 87%            |
| **Safety Anomaly Detection** | Real-time explanations<br/>Proactive threat prevention | ML anomaly detection + GenAI explanation<br/>Mandatory HITL for actions | HITL approval: 73%<br/>Prevented thefts: 47 in 6mo |

### Fleet Intelligence ⭐ NEW

| Use Case                            | Business Value                                          | Technical Approach                                                | Metrics                                              |
| ----------------------------------- | ------------------------------------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------- |
| **Demand Forecasting**              | Proactive positioning<br/>15% reduction in "no vehicle" | Time-series ML + historical data<br/>Weather & events integration | Forecast accuracy: 82%<br/>Availability: +15%        |
| **Fleet Rebalancing Optimization**  | Efficient crew routing<br/>30% faster rebalancing       | AI-driven route optimization<br/>Real-time demand integration     | Crew efficiency: +30%<br/>Rebalancing time: -25%     |
| **Battery Management Intelligence** | Prevent charge-outs<br/>Reduce swap crew overhead       | Predictive charge modeling<br/>Usage pattern analysis             | Charge-out incidents: -85%<br/>Swap efficiency: +40% |
| **Predictive Pre-Positioning**      | Commuter reliability<br/>Increase repeat usage          | User behavior ML<br/>Route-based anticipation                     | Commuter satisfaction: 4.7/5<br/>Repeat usage: +45%  |

### Customer Experience

| Use Case                    | Business Value                                       | Technical Approach                                                        | Metrics                               |
| --------------------------- | ---------------------------------------------------- | ------------------------------------------------------------------------- | ------------------------------------- |
| **Personalized Engagement** | Increased user retention<br/>Higher conversion rates | AI-driven user profiling & behavior analysis<br/>Tailored recommendations | Engagement: +28%<br/>Conversion: +18% |
| **Explainable Pricing**     | Transparent pricing<br/>Reduced disputes             | Dynamic pricing + NL explanation<br/>Evidence linking                     | Customer understanding: +35%          |

## Compliance & Governance

### EU AI Act Classification

**High-Risk System** ✓ (Vehicle safety control)

**Required Controls (All Implemented):**

- ✅ Risk Management System (TEVV Pipeline)
- ✅ Data Governance (Model Registry)
- ✅ Technical Documentation (ADRs + Model Cards)
- ✅ Record-Keeping (Audit Store)
- ✅ Transparency (Citations + Explanations)
- ✅ Human Oversight (HITL Gateway)
- ✅ Accuracy (96.2% factuality)
- ✅ Robustness (Adversarial testing)
- ✅ Cybersecurity (Prompt injection defense)

**See:** [EU AI Act Compliance](AI-Governance-Compliance/eu-ai-act-compliance.md)

## Resources

### Documentation

- 📊 [All Architecture Diagrams](resources/README.md)
- 📝 [Architecture Decision Records](Architecture-Decision-Records/)
- 🤖 [GenAI Strategy](GenAI-Strategy/)
- ⚖️ [Compliance Documentation](AI-Governance-Compliance/)

### External References

- [C4 Model](https://c4model.com/) - Architecture visualization
- [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) - AI risk management
- [EU AI Act](https://artificialintelligenceact.eu/) - AI regulation
- [O'Reilly Architecture Katas](https://learning.oreilly.com/live-events/architectural-katas/) - Competition info

## Team

- [Max Hopei](https://github.com/maxhopei)
- [Vanderlei Alves da Silva](https://github.com/vanderleisilva)
- [Yaroslav Poliakov](https://github.com/altersign)

---

**Competition:** O'Reilly Architecture Kata 2025
