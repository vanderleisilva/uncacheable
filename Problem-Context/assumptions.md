# Assumptions

## Business Assumptions

### Market & User Behavior

**ASSUME-BUS-001**: User acceptance of AI support

- **Assumption**: 70%+ of users will accept AI-powered conversational support if quality is high (96%+ accuracy) and human escalation is easy
- **Risk if wrong**: Low adoption → higher support costs, ROI not achieved
- **Validation**: User testing, pilot city metrics, NPS surveys

**ASSUME-BUS-002**: Cost savings materialization

- **Assumption**: GenAI conversational support will reduce support costs by 40% within 12 months
- **Risk if wrong**: Investment doesn't pay off, budget overruns
- **Validation**: Track support ticket deflection rate, cost per ticket, team size optimization

**ASSUME-BUS-003**: Competitive advantage window

- **Assumption**: AI-powered operations provide 18-24 month competitive advantage before competitors catch up
- **Risk if wrong**: Short-lived differentiation, pressure on pricing
- **Validation**: Monitor competitor AI launches, patent key innovations

**ASSUME-BUS-004**: Regulatory stability

- **Assumption**: EU AI Act requirements won't significantly change before 2026 enforcement
- **Risk if wrong**: Compliance rework, delays, additional costs
- **Validation**: Monitor regulatory updates, engage with legal counsel

**ASSUME-BUS-005**: Scaling economics

- **Assumption**: AI infrastructure costs scale sub-linearly (economies of scale with volume)
- **Risk if wrong**: Profitability declines as we scale
- **Validation**: Cost monitoring per city, per user, LLM provider volume pricing

### Growth Projections

**ASSUME-BUS-006**: City expansion pace

- **Assumption**: Will launch in 5 new cities within 18 months post-MVP
- **Risk if wrong**: Slower growth → longer ROI horizon
- **Validation**: Track pilot success, operational readiness

**ASSUME-BUS-007**: User retention improvement

- **Assumption**: AI-powered personalization will increase user retention by 15-25%
- **Risk if wrong**: Churn remains high, acquisition costs unsustainable
- **Validation**: Cohort analysis, A/B testing

## Technical Assumptions

### Fleet Intelligence & Demand Forecasting

**ASSUME-TECH-FLEET-001**: Historical data availability

- **Assumption**: Sufficient historical booking, telemetry, and location data exists (6+ months, 10K+ bookings per city)
- **Risk if wrong**: Poor ML model training, inaccurate demand forecasts
- **Validation**: Data audit before pilot, verify data quality and coverage

**ASSUME-TECH-FLEET-002**: Demand patterns are learnable

- **Assumption**: User demand follows predictable patterns based on time, location, weather, events (not random)
- **Risk if wrong**: ML models will be ineffective, wasted R&D investment
- **Validation**: Statistical analysis of historical data, pilot test forecast accuracy >70% baseline

**ASSUME-TECH-FLEET-003**: Battery charge is predictable

- **Assumption**: Battery depletion can be modeled from usage patterns, terrain, temperature
- **Risk if wrong**: Charge-out prevention fails, customer complaints continue
- **Validation**: Historical telemetry analysis, test charge prediction models

**ASSUME-TECH-FLEET-004**: External data sources accessible

- **Assumption**: Weather APIs, events calendars, public transit APIs are reliable and available
- **Risk if wrong**: Reduced forecast accuracy, missing key predictive signals
- **Validation**: Vendor evaluations, SLA reviews, fallback strategies

**ASSUME-TECH-FLEET-005**: Field crews will adopt AI routing

- **Assumption**: Battery swap crews and rebalancing teams will use AI-generated routes (not resist)
- **Risk if wrong**: Low adoption → no efficiency gains
- **Validation**: User research with field crews, pilot with early adopters, gather feedback

**ASSUME-TECH-FLEET-006**: Commuters have predictable patterns

- **Assumption**: Regular commuters use same routes/times consistently enough for pre-positioning
- **Risk if wrong**: Pre-positioning wastes resources on unpredictable users
- **Validation**: Analyze repeat user behavior, segment commuters vs. ad-hoc users

### AI/ML Capabilities

**ASSUME-TECH-001**: LLM factuality is sufficient

- **Assumption**: GPT-4 / Claude with RAG can achieve 96%+ factual accuracy for vehicle-sharing domain
- **Risk if wrong**: Too many hallucinations → user trust lost
- **Validation**: TEVV pipeline benchmarks, production monitoring

**ASSUME-TECH-002**: RAG reduces hallucinations

- **Assumption**: Retrieval-Augmented Generation reduces hallucination rate by 60-80% vs. vanilla LLM
- **Risk if wrong**: Insufficient accuracy, higher HITL overhead
- **Validation**: Hallucination detection metrics, A/B testing RAG vs. no-RAG

**ASSUME-TECH-003**: LLM provider SLA is reliable

- **Assumption**: LLM provider (OpenAI/Anthropic) maintains 99.9% uptime and consistent latency
- **Risk if wrong**: AI service frequently unavailable, user frustration
- **Validation**: Monitor provider SLA, implement fallback strategies

**ASSUME-TECH-004**: Context window is sufficient

- **Assumption**: 128K token context window (GPT-4 Turbo) is sufficient for RAG retrieval + conversation history
- **Risk if wrong**: Cannot provide enough context → reduced accuracy
- **Validation**: Monitor token usage, optimize retrieval size

**ASSUME-TECH-005**: Embedding model quality

- **Assumption**: OpenAI text-embedding-3-large or similar is sufficient for semantic search accuracy
- **Risk if wrong**: Poor retrieval quality → irrelevant context → bad responses
- **Validation**: Retrieval accuracy benchmarks, user feedback

### Infrastructure & Scalability

**ASSUME-TECH-006**: Managed Kafka handles scale

- **Assumption**: AWS MSK or Confluent Cloud can handle 10,000+ messages/sec without operational burden
- **Risk if wrong**: Kafka becomes bottleneck or operational nightmare
- **Validation**: Load testing, managed service SLA review

**ASSUME-TECH-007**: PostgreSQL scales per-service

- **Assumption**: Database-per-service with PostgreSQL is sufficient (no need for NoSQL)
- **Risk if wrong**: Database bottlenecks, scaling issues
- **Validation**: Load testing, read replicas, connection pooling

**ASSUME-TECH-008**: Cloud provider reliability

- **Assumption**: AWS/Azure/GCP provides 99.99% infrastructure uptime for multi-AZ deployments
- **Risk if wrong**: Frequent outages, SLA violations
- **Validation**: Leverage cloud provider SLAs, multi-region disaster recovery

**ASSUME-TECH-009**: GPU availability

- **Assumption**: Cloud GPU instances (e.g., AWS g5 instances) are readily available and cost-effective for GenAI Platform
- **Risk if wrong**: GPU shortages, cost overruns
- **Validation**: Reserved instances, capacity planning, consider managed LLM APIs

### Integration & APIs

**ASSUME-TECH-010**: Payment gateway reliability

- **Assumption**: Stripe or similar payment gateway provides 99.95% uptime and PCI-DSS compliance
- **Risk if wrong**: Payment failures, compliance issues
- **Validation**: Evaluate provider SLA, implement retry logic

**ASSUME-TECH-011**: Map services accuracy

- **Assumption**: Google Maps or similar provides accurate geocoding, routing, and ETA for all operational cities
- **Risk if wrong**: Poor user experience, incorrect ETAs
- **Validation**: Test coverage in target cities, fallback provider

**ASSUME-TECH-012**: IoT connectivity

- **Assumption**: Vehicles have sufficient cellular connectivity (4G/5G) for real-time telemetry
- **Risk if wrong**: Delayed telemetry, poor user experience
- **Validation**: Field testing, buffering strategies for offline periods

### Development & Deployment

**ASSUME-TECH-013**: Team can adopt microservices

- **Assumption**: Development team can successfully build and operate microservices architecture with event-driven communication
- **Risk if wrong**: Complexity overwhelms team, delays, quality issues
- **Validation**: Training, proof-of-concept, phased rollout

**ASSUME-TECH-014**: CI/CD for microservices

- **Assumption**: Can implement robust CI/CD pipeline with independent service deployments, zero downtime
- **Risk if wrong**: Deployment friction, frequent outages
- **Validation**: Infrastructure as code, automated testing, canary deployments

**ASSUME-TECH-015**: Observability tooling is sufficient

- **Assumption**: Prometheus + Grafana + Jaeger provide adequate observability for microservices + GenAI
- **Risk if wrong**: Blind spots, slow incident resolution
- **Validation**: Observability pilot, incident drills

## Regulatory & Compliance Assumptions

### EU AI Act Compliance

**ASSUME-REG-001**: High-risk classification is correct

- **Assumption**: MobilityCorp's GenAI system correctly classifies as "high-risk" under EU AI Act (safety-critical vehicle operations)
- **Risk if wrong**: Incorrect compliance posture, audit failures
- **Validation**: Legal review, regulatory consultation

**ASSUME-REG-002**: Audit trails are sufficient

- **Assumption**: 90-day retention of immutable AI decision logs satisfies EU AI Act record-keeping requirements
- **Risk if wrong**: Compliance failure, fines
- **Validation**: Legal review, mock audits

**ASSUME-REG-003**: HITL implementation meets requirements

- **Assumption**: Implemented HITL gates for high-risk decisions satisfy "human oversight" requirement
- **Risk if wrong**: Compliance gaps, regulatory action
- **Validation**: Legal review, document HITL processes

**ASSUME-REG-004**: Model cards provide sufficient transparency

- **Assumption**: Model cards documenting purpose, limitations, performance satisfy EU AI Act transparency requirements
- **Risk if wrong**: Insufficient documentation for audits
- **Validation**: Template review with legal team, peer benchmarking

### Data Privacy (GDPR)

**ASSUME-REG-005**: Anonymization is effective

- **Assumption**: Anonymization techniques prevent re-identification of users in analytics data
- **Risk if wrong**: GDPR violation, fines
- **Validation**: Privacy impact assessment, third-party review

**ASSUME-REG-006**: Consent management is sufficient

- **Assumption**: Implemented consent framework satisfies GDPR granular consent requirements
- **Risk if wrong**: Non-compliance, user complaints
- **Validation**: Legal review, user testing

**ASSUME-REG-007**: Right to erasure is compliant

- **Assumption**: 30-day data deletion process satisfies GDPR "right to erasure"
- **Risk if wrong**: GDPR violations
- **Validation**: Legal review, test deletion workflows

## Operational Assumptions

### Support & Operations

**ASSUME-OPS-001**: Operations team capacity

- **Assumption**: Existing 8-person support team + 5 field technicians can handle HITL workload and escalations
- **Risk if wrong**: Overwhelmed team, SLA violations
- **Validation**: Monitor HITL approval times, escalation rates

**ASSUME-OPS-002**: HITL response time achievable

- **Assumption**: Operations team can review and approve/reject high-risk AI decisions within 5 minutes p95
- **Risk if wrong**: Delays, user frustration, safety risks
- **Validation**: Pilot testing, measure response times

**ASSUME-OPS-003**: Multi-language support quality

- **Assumption**: LLMs can provide high-quality responses in English, German, French, Dutch
- **Risk if wrong**: Poor non-English user experience
- **Validation**: Language-specific benchmarks, native speaker review

### Monitoring & Incident Response

**ASSUME-OPS-004**: Incident detection is timely

- **Assumption**: Safety anomalies are detected within 30 seconds of occurrence
- **Risk if wrong**: Delayed incident response, safety risks
- **Validation**: Telemetry pipeline latency testing

**ASSUME-OPS-005**: False positive rate is acceptable

- **Assumption**: AI anomaly detection false positive rate <10%
- **Risk if wrong**: Alert fatigue, missed real incidents
- **Validation**: Tune models, A/B testing, production metrics

## Data Assumptions

### Data Quality

**ASSUME-DATA-001**: Historical data is sufficient for RAG

- **Assumption**: Existing support documentation, incident reports, and policies provide sufficient corpus for RAG
- **Risk if wrong**: Poor retrieval quality, irrelevant context
- **Validation**: Document audit, gap analysis, synthetic data generation

**ASSUME-DATA-002**: Telemetry data is reliable

- **Assumption**: Vehicle telemetry (GPS, battery, sensors) is accurate and timely
- **Risk if wrong**: Incorrect fleet analytics, poor incident detection
- **Validation**: Field testing, calibration, anomaly detection

**ASSUME-DATA-003**: User data for personalization

- **Assumption**: Sufficient user behavior data exists to train personalization models
- **Risk if wrong**: Generic recommendations, low engagement lift
- **Validation**: Data availability assessment, cold-start strategies

### Data Volume

**ASSUME-DATA-004**: Telemetry volume projection

- **Assumption**: Peak telemetry volume is 10,000 messages/sec (based on 5,000 active vehicles × 2 messages/sec)
- **Risk if wrong**: Under-provisioned infrastructure, message loss
- **Validation**: Extrapolate from pilot city data, stress testing

**ASSUME-DATA-005**: AI interaction volume

- **Assumption**: 20% of users will use conversational support daily, averaging 2 interactions/day
- **Risk if wrong**: Cost overruns or under-utilized infrastructure
- **Validation**: User surveys, pilot city metrics

## External Assumptions

### Vendor & Partner Reliability

**ASSUME-EXT-001**: LLM provider stability

- **Assumption**: OpenAI or Anthropic will remain viable vendors for next 3+ years
- **Risk if wrong**: Forced migration, service disruption
- **Validation**: Diversification strategy, abstraction layer

**ASSUME-EXT-002**: Payment gateway partnership

- **Assumption**: Stripe or similar maintains competitive pricing and feature set
- **Risk if wrong**: Cost increases, feature gaps
- **Validation**: Multi-year contract, competitive evaluation

**ASSUME-EXT-003**: Map services availability

- **Assumption**: Google Maps or similar remains available and affordable
- **Risk if wrong**: Service disruption, cost overruns
- **Validation**: Contract terms, fallback provider

### Regulatory Environment

**ASSUME-EXT-004**: No major regulatory changes

- **Assumption**: No major new regulations beyond EU AI Act in next 18 months
- **Risk if wrong**: Compliance rework, project delays
- **Validation**: Regulatory monitoring, industry associations

**ASSUME-EXT-005**: City-level regulations remain stable

- **Assumption**: City-specific vehicle-sharing regulations don't significantly tighten
- **Risk if wrong**: Operational restrictions, reduced profitability
- **Validation**: Government relations, industry advocacy

## Validation Strategy

For each critical assumption:

1. **Document explicitly**: Capture assumption in this document
2. **Assign risk level**: High, Medium, Low
3. **Define validation approach**: How will we test this assumption?
4. **Set validation timeline**: When must we validate?
5. **Establish contingency**: What's Plan B if assumption proves wrong?

### High-Priority Assumptions to Validate Early

1. **ASSUME-TECH-001**: LLM factuality (validate in first 2 months via TEVV)
2. **ASSUME-BUS-001**: User acceptance of AI (pilot testing in month 3-4)
3. **ASSUME-TECH-002**: RAG effectiveness (validate in first month via benchmarks)
4. **ASSUME-OPS-002**: HITL response time (pilot in month 4-5)
5. **ASSUME-REG-001**: EU AI Act classification (legal review by month 2)

---

## Living Document

This assumptions document is a **living document** and should be:

- Reviewed monthly during project execution
- Updated as assumptions are validated or invalidated
- Used to drive risk mitigation planning
- Referenced in ADRs when assumptions influence decisions

**Last Updated**: 2025-10-18
