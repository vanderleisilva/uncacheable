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

- **Runtime Validation**: Multi-layer quality checks (hallucination detection, confidence calibration, factuality verification) on every AI response
- **Model Monitoring**: Real-time drift detection, hallucination tracking, and performance degradation alerts
- **Provider Resilience**: Abstraction layer for LLM providers, shadow mode testing, and graceful degradation strategies
- **Compliance by Design**: EU AI Act compliance with immutable audit trails, model registry, and human oversight

**Customer Experience:**

- **Personalized Engagement**: Tailored recommendations based on individual usage patterns to increase retention
- **Transparent Pricing**: Natural language explanations for dynamic pricing to build customer trust

**Architectural Differentiator**: Our GenAI Platform operates as an **isolated, observable subsystem** with built-in safeguards—RAG grounding prevents hallucinations, runtime validation ensures quality, immutable audit trails provide compliance, and HITL gates enforce human oversight for safety-critical decisions. This bounded context approach allows us to innovate rapidly with AI while maintaining EU AI Act compliance for high-risk vehicle operations.

## Quick Navigation

### 📋 Problem & Requirements

- [Problem Context](Problem-Context/) - Business case, actors, and constraints
  - [Business Case](Problem-Context/business-case.md)
  - [Requirements](Problem-Context/requirements.md)
  - [Actors & Personas](Problem-Context/actors-and-personas.md)
  - [Constraints](Problem-Context/constraints.md)
  - [Assumptions](Problem-Context/assumptions.md)

### 🤖 GenAI Strategy (Our Differentiator)

- **[GenAI Strategy](GenAI-Strategy/README.md)** ⭐ **START HERE** - Complete AI strategy overview
  - Why GenAI breaks the cost-scaling paradox
  - Three strategic domains (Fleet Intelligence, Operations & Safety, Customer Experience)
  - Our competitive edge (RAG, Runtime Validation, HITL, Compliance by Design)
  - EU AI Act high-risk classification and mandatory controls
  - Architecture integration as isolated bounded context

### ⚖️ AI Governance & Compliance

- [AI Governance & Compliance](AI-Governance-Compliance/) - **EU AI Act compliance**
  - [Compliance & Governance Framework](AI-Governance-Compliance/compliance-framework.md) ⭐
    - EU AI Act compliance (risk classification, required controls)
    - Model registry & audit trail design
    - Governance processes & responsibilities
  - [AI Model Documentation](AI-Governance-Compliance/model-cards.md) ⭐
    - Model cards for all AI models (Conversational Support, Incident Classifier, Safety Detector)
    - Training data provenance & performance metrics
    - Model limitations & bias testing
  - [Security & Privacy](AI-Governance-Compliance/security-privacy.md)
    - GDPR compliance & data protection
    - AI-specific security (prompt injection, adversarial attacks)
    - Access controls & encryption

### 🎯 Quality Attributes & Targets

**Key quality goals and how we achieve them:**

- **Scalability**: Independent service scaling, event-driven architecture, horizontal pod autoscaling
- **Availability**: 99.9% uptime per service, multi-AZ deployment, circuit breakers, graceful degradation
- **Security**: Zero-trust architecture, encryption at rest/transit, RBAC, prompt injection defense
- **AI Safety**: Multi-layer runtime validation, HITL gates for high-risk decisions, continuous monitoring ⭐
- **Explainability**: Natural language explanations, source citations, confidence scores ⭐
- **Cost Efficiency**: Managed services, auto-scaling, LLM provider abstraction

**See ADRs for detailed tradeoffs and rationale**

## Architecture Overview

### 📝 Architecture Decision Records

- [Architecture Decision Records](Architecture-Decision-Records/) - **Critical decisions, rationale & tradeoffs**
  - [ADR Template](Architecture-Decision-Records/000-adr-template.md) - Standard format for new ADRs
  - [ADR-001: Combine Microservices, Streaming, and Agentic Architectures for the holistic solution](Architecture-Decision-Records/001-high-level-architecture.md)
  - [ADR-002: Microservices Architecture](Architecture-Decision-Records/002-microservices-architecture.md)
  - [ADR-003: Event-Driven Backbone](Architecture-Decision-Records/003-event-driven-backbone.md)
  - [ADR-004: Core Services Architecture](Architecture-Decision-Records/004-core-services-decomposition.md)
  - [ADR-005: RAG Strategy](Architecture-Decision-Records/005-rag-strategy.md) ⭐

_Note: Each ADR includes detailed consequences, risks, and mitigation strategies_

### 🎨 Architecture Views & Diagrams

- **Visual documentation**
  - [Context Diagram](resources/diagrams/context/context-diagram.md) - System boundary
  - [Container Diagram](resources/diagrams/container/container-diagram.md) - High-level components
  - [Core Services Diagram](resources/diagrams/container/core-services-container-diagram.md) - Detailed service decomposition
  - [GenAI Component Diagram](resources/diagrams/genai-subsystem/genai-component-diagram.md) ⭐ - Runtime validation & quality gates
  - [RAG Data Flow](resources/diagrams/data-flow/rag-data-flow.md) ⭐
  - **Key AI Flows**:
    - [Conversational Support](resources/diagrams/use-cases/conversational-support-flow.md) ⭐
    - [Predictive Fleet Positioning](resources/diagrams/use-cases/predictive-fleet-positioning.md) ⭐
    - [Safety Anomaly Detection](resources/diagrams/use-cases/safety-anomaly-detection-flow.md) ⭐

### GenAI Platform Architecture

The GenAI Platform is our key differentiator, implementing responsible AI with safety controls:

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

- ✅ Risk Management System (Runtime validation + pre-deployment testing)
- ✅ Data Governance (Model Registry)
- ✅ Technical Documentation (ADRs + Model Cards)
- ✅ Record-Keeping (Audit Store)
- ✅ Transparency (Citations + Explanations)
- ✅ Human Oversight (HITL Gateway)
- ✅ Accuracy (96.2% factuality)
- ✅ Robustness (Continuous monitoring + shadow testing)
- ✅ Cybersecurity (Prompt injection defense)

**See:** [Compliance & Governance Framework](AI-Governance-Compliance/compliance-framework.md)

## External References

- [C4 Model](https://c4model.com/) - Architecture visualization
- [NIST AI RMF](https://www.nist.gov/itl/ai-risk-management-framework) - AI risk management
- [EU AI Act](https://artificialintelligenceact.eu/) - AI regulation

## Team

- [Max Hopei](https://github.com/maxhopei)
- [Vanderlei Alves da Silva](https://github.com/vanderleisilva)
- [Yaroslav Poliakov](https://github.com/altersign)

---

**Competition:** O'Reilly Architecture Kata 2025
