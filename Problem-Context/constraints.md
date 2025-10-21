# Constraints

## Technical Constraints

### Infrastructure

**CONST-INFRA-001**: Cloud-based deployment

- Must deploy on major cloud provider (AWS, Azure, or GCP)
- No on-premises infrastructure requirement
- Multi-region capability required for EU data residency

**CONST-INFRA-002**: Technology stack maturity

- Use proven, production-ready technologies
- Avoid experimental frameworks
- Priority: Node.js, Python, Go for services
- PostgreSQL for relational data, Redis for caching

**CONST-INFRA-003**: GPU infrastructure for GenAI

- GenAI service requires GPU-enabled compute nodes
- Cost constraint: GPU usage must be optimized
- Consider managed LLM APIs vs. self-hosted models

### Integration

**CONST-INT-001**: External API dependencies

- Payment gateway: Must be PCI-DSS Level 1 certified
- Map services: Must support European coverage
- LLM provider: Must offer enterprise SLA and data privacy guarantees

**CONST-INT-002**: IoT protocol standardization

- Vehicle telemetry must use MQTT protocol (industry standard)
- Support for intermittent connectivity
- Message queuing for offline vehicles

**CONST-INT-003**: Backward compatibility

- Existing mobile apps (iOS, Android) must continue to work
- API versioning required for gradual migration
- No breaking changes to customer-facing features

### Performance

**CONST-PERF-001**: Response time requirements

- User-facing APIs: <500ms p95
- GenAI conversational support: <2s p95
- Search/availability queries: <300ms p95

**CONST-PERF-002**: Scalability targets

- Must handle 10,000+ concurrent users per city
- Support 5-10x traffic spikes during events
- Horizontal scaling required (no vertical scaling bottlenecks)

**CONST-PERF-003**: Telemetry ingestion capacity

- Must handle 10,000+ telemetry messages per second at peak
- Latency: <1s from vehicle to storage
- No message loss for critical events (incidents, anomalies)

### Data & Storage

**CONST-DATA-001**: Data residency

- EU user data must remain in EU regions (GDPR requirement)
- GenAI training data must not leave approved regions
- Cross-region replication for disaster recovery only

**CONST-DATA-002**: Data retention

- Operational logs: 30 days
- AI audit logs: 90 days minimum (EU AI Act requirement)
- User data: Indefinite (until account deletion)
- Telemetry data: 7 days hot storage, 90 days cold storage

**CONST-DATA-003**: Database per service

- No shared databases between microservices
- Each service owns its data
- Event-driven integration for data sharing

## Regulatory & Compliance Constraints

### EU AI Act Compliance

**CONST-REG-001**: High-risk AI system classification

- MobilityCorp's GenAI service qualifies as "high-risk" (safety-critical vehicle operations)
- Must implement all EU AI Act requirements:
  - ✅ Risk management system
  - ✅ Data governance and quality
  - ✅ Technical documentation
  - ✅ Record-keeping (audit trails)
  - ✅ Transparency and user information
  - ✅ Human oversight
  - ✅ Accuracy, robustness, cybersecurity

**CONST-REG-002**: Mandatory human oversight

- High-risk AI decisions must have human-in-the-loop (HITL) gates
- Example: AI-triggered vehicle immobilization requires human approval
- Operations team must have override capability
- Response time for HITL approval: <5 minutes target

**CONST-REG-003**: Audit trail requirements

- All GenAI interactions must be logged immutably
- Logs must include: input, output, model version, confidence score, timestamp
- Retention: 90 days minimum
- Must be queryable for regulatory audits

**CONST-REG-004**: Transparency requirements

- Users must be informed when interacting with AI
- AI responses must include source citations
- Users must have right to opt out of AI-driven personalization
- Explainability: AI decisions must be explainable in natural language

### Data Privacy (GDPR)

**CONST-PRIV-001**: User consent management

- Explicit opt-in required for AI personalization
- Granular consent for data processing purposes
- Easy withdrawal of consent

**CONST-PRIV-002**: Data minimization

- Collect only necessary data
- Anonymize data for analytics when possible
- No PII in GenAI prompts (privacy-preserving AI)

**CONST-PRIV-003**: Right to erasure

- Users can request account and data deletion
- Data must be deleted within 30 days
- Audit logs exempt (regulatory requirement)

**CONST-PRIV-004**: Data encryption

- Data at rest: AES-256 encryption
- Data in transit: TLS 1.3
- Key management via cloud provider KMS

### Payment Processing (PCI-DSS)

**CONST-PAY-001**: No card data storage

- Use tokenization via payment gateway
- Never store full credit card numbers
- PCI-DSS Level 1 certified payment provider required

**CONST-PAY-002**: Secure payment flow

- TLS for all payment API calls
- 3D Secure for European cards
- Fraud detection integration

### Accessibility

**CONST-ACC-001**: WCAG 2.1 Level AA compliance

- Mobile app and web dashboard must be accessible
- Screen reader support
- Keyboard navigation support

## Business Constraints

### Budget

**CONST-BUD-001**: Development budget

- Limited to existing development team (no unlimited hiring)
- Phased rollout required to spread costs
- Leverage managed services to reduce operational overhead

**CONST-BUD-002**: Infrastructure costs

- Cloud infrastructure budget must be managed per city deployment
- GenAI inference costs: Target cost-effective per-interaction pricing
- Optimize GPU usage (batch processing, caching) to control costs

**CONST-BUD-003**: Third-party costs

- LLM API costs: Negotiate volume pricing with providers
- Payment gateway fees: Industry-standard transaction fees apply
- Map services: Optimize API call frequency to control costs

### Timeline

**CONST-TIME-001**: MVP delivery

- Phase 1 (Conversational Support MVP): 6 months target
- Phased rollout required (cannot launch all features simultaneously)
- Early validation with pilot city before scaling

**CONST-TIME-002**: Market pressure

- Competitors are launching AI features
- Must demonstrate AI value within 12 months
- Cannot delay indefinitely for "perfect" solution

### Team & Skills

**CONST-TEAM-001**: Limited AI/ML expertise

- Small AI/ML team (2-3 engineers initially)
- Must leverage managed LLM services (not train from scratch)
- Upskilling required for RAG, prompt engineering, TEVV

**CONST-TEAM-002**: DevOps capacity

- 4-person DevOps team managing entire platform
- Operational complexity must be manageable
- Prefer managed services over self-hosted where feasible

**CONST-TEAM-003**: Distributed team

- Team distributed across EU (Amsterdam, Berlin, Paris)
- Asynchronous collaboration required
- Documentation-first culture essential

## Operational Constraints

### Availability

**CONST-OPS-001**: Uptime requirements

- Core platform: 99.9% uptime (43 minutes downtime/month allowed)
- GenAI service: 99.5% uptime (degraded mode acceptable)
- Graceful degradation when GenAI unavailable

**CONST-OPS-002**: Maintenance windows

- No maintenance windows during peak hours (7-9 AM, 5-7 PM)
- Zero-downtime deployments required
- Canary deployments for risk mitigation

### Support

**CONST-SUPPORT-001**: 24/7 operations team

- Operations team available for HITL approvals 24/7
- Escalation path for critical issues
- Maximum 5-minute response time for high-priority incidents

**CONST-SUPPORT-002**: Multi-language support

- Conversational AI must support: English, German, French, Dutch
- Fallback to English if language detection fails
- Human support available in all supported languages

### Security

**CONST-SEC-001**: Security audits

- Annual third-party security audit required
- Penetration testing before major releases
- Bug bounty program for vulnerability disclosure

**CONST-SEC-002**: AI security

- Prompt injection testing mandatory
- Adversarial robustness testing for GenAI models
- Rate limiting to prevent abuse

**CONST-SEC-003**: Incident response

- Security incident response plan required
- <4 hour response time for critical vulnerabilities
- Post-incident review and documentation

## Domain Constraints

### Vehicle Sharing Industry

**CONST-DOMAIN-001**: Insurance requirements

- Insurance provider requires telemetry data retention
- Real-time incident reporting to insurers
- Vehicle tracking for theft recovery

**CONST-DOMAIN-002**: Local regulations

- Compliance with city-specific vehicle-sharing regulations
- Parking zone restrictions (geofencing)
- Speed limits enforcement
- Helmet requirements (varies by city and vehicle type)

**CONST-DOMAIN-003**: Vehicle safety standards

- Vehicles must meet local safety certifications
- Regular maintenance schedules mandated
- Safety inspection records required

### Multi-Vehicle Type Complexity

**CONST-VEHICLE-001**: Vehicle heterogeneity

- Four vehicle types with different characteristics:
  - Scooters: Low battery, high turnover, low cost
  - eBikes: Medium battery, medium turnover, medium cost
  - Cars: High battery, low turnover, high cost, insurance complexity
  - Vans: Highest battery, lowest turnover, highest cost, commercial use
- Different regulatory requirements per type
- Different pricing models

**CONST-VEHICLE-002**: Licensing requirements

- Driver's license verification for cars/vans
- Age verification (18+ for cars/vans, 16+ for scooters/bikes)
- International license support

## Technology Constraints

### AI/ML Limitations

**CONST-AI-001**: LLM limitations

- LLMs can hallucinate (generate false information)
- Context window limits (e.g., 128K tokens for GPT-4)
- Cost per token constraints
- Latency: 1-3 seconds for LLM inference

**CONST-AI-002**: RAG limitations

- Vector search quality depends on embedding model
- Index size grows with document corpus
- Re-indexing required for knowledge updates
- Not suitable for real-time data (telemetry)

**CONST-AI-003**: Explainability tradeoff

- More complex models → harder to explain
- Must balance accuracy vs. explainability
- EU AI Act requires explainability for high-risk systems

### Vendor Lock-in Risks

**CONST-VENDOR-001**: LLM provider dependency

- Switching LLM providers is costly (re-training, re-tuning)
- Model-specific prompt engineering
- Mitigate with abstraction layer

**CONST-VENDOR-002**: Cloud provider dependency

- Multi-cloud is expensive and complex
- Accept single-cloud with disaster recovery plan
- Avoid proprietary services for critical paths

## Summary: Constraint Impact on Architecture

| Constraint Type           | Key Impact on Architecture                                      |
| ------------------------- | --------------------------------------------------------------- |
| **EU AI Act**             | GenAI as isolated bounded context with audit trails, HITL gates |
| **GDPR**                  | Privacy-preserving AI (no PII in prompts), data residency       |
| **Performance**           | Event-driven architecture, caching, horizontal scaling          |
| **Budget**                | Managed services, phased rollout, cost monitoring               |
| **Team Size**             | Microservices with clear boundaries, managed Kafka/LLM          |
| **Vehicle Heterogeneity** | Flexible data model, service abstraction per vehicle type       |
| **AI Limitations**        | RAG for grounding, hallucination detection, HITL for high-risk  |

These constraints shape the fundamental architectural decisions documented in ADRs and guide implementation priorities throughout the project.
