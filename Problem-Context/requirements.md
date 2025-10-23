# Functional Requirements

## Core Platform Requirements

### Vehicle Management

**REQ-VM-001**: Support multiple vehicle types

- Electric scooters
- eBikes
- Electric cars
- Vans

**REQ-VM-002**: Real-time vehicle tracking

- GPS location updates every 10-30 seconds
- Battery level monitoring
- Lock/unlock status
- In-use vs. available state

**REQ-VM-003**: Vehicle availability search

- Search by location (radius-based)
- Filter by vehicle type
- Show real-time availability
- Display estimated walking distance

**REQ-VM-004**: Vehicle control

- Remote lock/unlock via mobile app
- Emergency immobilization capability
- Battery status alerts
- Maintenance mode activation

### Booking & Rides

**REQ-BR-001**: Vehicle reservation

- Reserve available vehicle for 10 minutes
- Cancel reservation without penalty (within time window)
- Automatic reservation expiry

**REQ-BR-002**: Ride lifecycle management

- Start ride (unlock vehicle)
- Track active ride duration
- End ride (lock vehicle)
- Post-ride summary with route and cost

**REQ-BR-003**: Pricing & billing

- Dynamic pricing based on vehicle type, duration, distance
- Transparent pricing display before ride start
- Automated payment processing at ride end
- Support for promotions and discounts

**REQ-BR-004**: Ride history

- View past rides with details
- Download receipts
- Dispute charges

### User Management

**REQ-UM-001**: User registration & authentication

- Email/phone registration
- Multi-factor authentication
- Identity verification (driver's license for cars/vans)
- Age verification (18+ for cars/vans, 16+ for scooters/bikes)

**REQ-UM-002**: User profiles

- Personal information management
- Payment methods (credit card, digital wallets)
- Ride preferences
- Communication preferences

**REQ-UM-003**: User segmentation

- Commuter vs. tourist vs. occasional user
- Usage patterns for personalization
- Risk scoring for safety

### Payment Processing

**REQ-PM-001**: Payment method management

- Add/remove payment methods
- Default payment method selection
- Payment method validation

**REQ-PM-002**: Payment processing

- Pre-authorization hold before ride
- Automatic charge on ride completion
- Refund processing for disputes
- Failed payment retry logic

**REQ-PM-003**: Invoicing

- Digital receipts
- Monthly statements for frequent users
- Tax-compliant invoicing

## GenAI-Powered Requirements ⭐

### Fleet Intelligence

**REQ-AI-FLEET-001**: Demand forecasting

- Predict vehicle demand by location, time of day, day of week
- Integrate external factors (weather, events, public transit status)
- Generate demand heatmaps for operational planning
- Forecast accuracy: >80%
- Update frequency: Every 15 minutes for real-time, daily for strategic planning

**REQ-AI-FLEET-002**: Fleet rebalancing optimization

- Generate optimal vehicle redistribution plans
- Optimize field crew routes for efficiency
- Balance demand predictions with current distribution
- Prioritize rebalancing tasks by impact
- Route optimization: 30%+ crew efficiency improvement

**REQ-AI-FLEET-003**: Battery management intelligence

- Predict charge depletion based on usage patterns
- Prioritize battery swap locations by urgency and impact
- Prevent bookings when insufficient charge for trip duration
- Generate battery swap crew routes
- Target: 85%+ reduction in charge-out incidents

**REQ-AI-FLEET-004**: Predictive pre-positioning

- Analyze commuter usage patterns for regular users
- Anticipate vehicle needs for frequent routes
- Pre-position vehicles for high-value repeat customers
- Notify users of guaranteed vehicle availability
- Target: 45%+ increase in repeat commuter usage

**REQ-AI-FLEET-005**: Fleet analytics & insights

- Identify underutilized vs. over-demand zones
- Analyze vehicle type preferences by location and time
- Detect seasonal and event-driven demand patterns
- Generate actionable recommendations for fleet composition
- Dashboard with real-time and historical insights

### Conversational Support

**REQ-AI-001**: Natural language customer support

- Answer common questions (pricing, how-to, policies)
- Troubleshooting assistance (app issues, vehicle problems)
- Account-related queries
- Response time: <2 seconds p95

**REQ-AI-002**: Citation & transparency

- All AI responses must include source citations
- "Powered by AI" disclosure on every response
- Easy escalation to human support
- Confidence score display for responses

**REQ-AI-003**: Factuality & accuracy

- 96%+ factual accuracy for responses
- Hallucination detection and blocking
- Graceful failure with human escalation

### Incident Management

**REQ-AI-004**: Automated incident summarization

- Generate incident summary from telemetry, images, user reports
- Identify similar historical incidents via RAG
- Suggest resolution actions based on past incidents
- Generate time: <10 seconds
- See [Incident Summarization use case](../resources/diagrams/use-cases/incident-summarization.md) for detailed flow

**REQ-AI-005**: Incident classification

- Categorize incidents: accident, theft, vandalism, mechanical failure
- Severity scoring: low, medium, high, critical
- Automatic routing to appropriate team

### Safety & Anomaly Detection

**REQ-AI-006**: Real-time safety anomaly detection

- Detect unusual patterns: sudden stops, location anomalies, speed violations
- Generate natural language explanations for anomalies
- Risk assessment scoring

**REQ-AI-007**: Human-in-the-loop for high-risk actions

- Flag high-risk AI decisions for human review
- Mandatory approval for vehicle immobilization decisions
- Track approval/rejection metrics
- Approval turnaround: <5 minutes p95

### Personalized Engagement

**REQ-AI-008**: User behavior analysis

- Analyze usage patterns for personalization
- Privacy-preserving analysis (no PII in AI models)
- Consent-based data usage

**REQ-AI-009**: Tailored recommendations

- Vehicle type recommendations based on usage
- Route suggestions
- Timing recommendations for best availability
- Promotional offers aligned with user preferences

**REQ-AI-010**: Engagement optimization

- Increase user retention through personalized interactions
- Reduce churn through proactive engagement
- Measure engagement lift: target +25%

## Operational Requirements

### Fleet Operations Dashboard

**REQ-OP-001**: Real-time fleet monitoring

- Vehicle locations on map
- Battery levels and alerts
- Active rides visualization
- Incident alerts

**REQ-OP-002**: Fleet analytics

- Utilization rates by vehicle type
- Popular locations and routes
- Maintenance predictions
- Revenue analytics

**REQ-OP-003**: Operations team tools

- Incident management interface
- HITL approval interface for AI decisions
- Vehicle redistribution planning
- Maintenance scheduling

### Telemetry & IoT

**REQ-IOT-001**: Telemetry ingestion

- Ingest 10,000+ messages/second at peak
- Process location, battery, speed, lock status, sensor data
- Handle intermittent connectivity
- Store time-series data efficiently

**REQ-IOT-002**: Vehicle-to-platform communication

- MQTT protocol for IoT messaging
- Secure device authentication
- Command delivery (lock/unlock)
- Firmware update capability

## Compliance & Governance Requirements

### EU AI Act Compliance ⭐

**REQ-COMP-001**: High-risk AI system classification

- Document risk assessment for safety-critical AI
- Implement required controls per EU AI Act
- Regular compliance audits

**REQ-COMP-002**: AI audit trails

- Immutable logs for all AI requests and responses
- Retain for 90 days minimum
- Include input, output, model version, confidence scores
- Queryable for regulatory audits

**REQ-COMP-003**: Model documentation

- Model cards for each AI model
- Training data provenance
- Performance metrics and limitations
- Bias testing results

**REQ-COMP-004**: Human oversight

- HITL gates for high-risk decisions
- Human approval tracking
- Override capability for AI decisions

**REQ-COMP-005**: Transparency & explainability

- Explain AI decisions in natural language
- Provide source attribution (citations)
- Disclose AI usage to users
- Right to opt-out of AI-driven personalization

### Data Privacy

**REQ-PRIV-001**: GDPR compliance

- User consent management
- Data minimization
- Right to access, rectify, delete
- Data portability

**REQ-PRIV-002**: Privacy-preserving AI

- No PII in LLM prompts
- Anonymization for analytics
- Encrypted data at rest and in transit

### Security

**REQ-SEC-001**: Authentication & authorization

- Role-based access control (RBAC)
- API authentication (OAuth 2.0)
- Session management

**REQ-SEC-002**: AI security

- Prompt injection detection and blocking
- Input validation and sanitization
- Rate limiting for AI endpoints
- Adversarial testing

**REQ-SEC-003**: Data security

- Encryption at rest (AES-256)
- TLS 1.3 for data in transit
- Secure key management
- Regular security audits

## Non-Functional Requirements

### Performance

**REQ-PERF-001**: Response times

- Vehicle search: <500ms p95
- Booking creation: <500ms p95
- AI conversational support: <2s p95
- AI incident summarization: <10s p95

**REQ-PERF-002**: Throughput

- Support 10,000+ concurrent users per city
- Handle 100+ bookings per minute
- Process 10,000+ telemetry messages per second

### Availability

**REQ-AVAIL-001**: System uptime

- Core platform: 99.9% uptime (43 minutes downtime/month)
- GenAI Platform: 99.5% uptime (degraded support acceptable)
- Payment processing: 99.95% uptime

**REQ-AVAIL-002**: Graceful degradation

- GenAI Platform failure → escalate to human support
- Payment gateway failure → queue for retry
- Telemetry ingestion buffering during outages

### Scalability

**REQ-SCALE-001**: Horizontal scaling

- Auto-scale based on demand
- Support 5-10x traffic spikes during events
- Scale services independently

**REQ-SCALE-002**: Geographic expansion

- Multi-region deployment capability
- Low-latency within each region (<100ms)
- Data residency compliance

### Observability

**REQ-OBS-001**: Monitoring & alerting

- Real-time metrics for all services
- AI-specific metrics: hallucination rate, confidence scores, HITL approval rate
- Automated alerting for anomalies
- SLO-based dashboards

**REQ-OBS-002**: Distributed tracing

- End-to-end request tracing
- Performance bottleneck identification
- AI decision provenance tracking

**REQ-OBS-003**: Logging

- Centralized log aggregation
- Structured logging (JSON)
- Log retention: 30 days operational, 90 days AI audit logs

## Integration Requirements

**REQ-INT-001**: Payment gateway integration

- Stripe or similar payment processor
- PCI-DSS compliant handling
- Support for multiple currencies

**REQ-INT-002**: Map services integration

- Google Maps or similar for routing and locations
- Geocoding and reverse geocoding
- Distance/duration calculations

**REQ-INT-003**: LLM provider integration

- OpenAI GPT-4 or Anthropic Claude
- API rate limiting and fallback
- Model version management

**REQ-INT-004**: Notification services

- Push notifications (mobile)
- Email notifications
- SMS for critical alerts

## Success Metrics

- **User Satisfaction**: AI support NPS >40 (vs. human support baseline)
- **Support Cost**: 40% reduction in per-user support costs
- **Incident Resolution**: 10x faster incident investigation time
- **AI Accuracy**: 96%+ factual accuracy for AI responses
- **Safety**: 50+ prevented theft/vandalism incidents per city annually
- **Compliance**: Zero EU AI Act violations
- **Uptime**: Meet or exceed 99.9% platform availability
