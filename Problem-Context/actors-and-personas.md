# Actors & Personas

## Primary Actors

### 1. Customers (End Users)

Users of the vehicle-sharing platform with varying needs and behaviors.

#### Persona: "Commuter Clara"

**Profile:**

- Age: 28, Marketing Manager
- Location: Berlin, Germany
- Usage: Daily commuter (home ↔ office)
- Preferred vehicle: eBike

**Goals:**

- Quick, reliable transportation to/from work
- Predictable costs and availability
- Minimal friction in booking and payment

**Pain Points:**

- Vehicle availability during rush hour
- Uncertainty about pricing (dynamic)
- Need immediate support for issues

**AI Interaction:**

- Frequent user of conversational support for quick questions
- Appreciates personalized vehicle recommendations
- Values fast response times (<2s)
- High trust in AI if accuracy is maintained

**Key Scenarios:**

- "Where's the nearest eBike with 50%+ battery?"
- "Why was I charged €12 instead of the usual €8?"
- "My eBike won't unlock—help!"

---

#### Persona: "Tourist Tom"

**Profile:**

- Age: 35, Software Engineer from San Francisco
- Location: Amsterdam (visiting for a week)
- Usage: Occasional user for sightseeing
- Preferred vehicle: Electric scooter or eBike

**Goals:**

- Easy signup and first-time use
- Explore city flexibly without public transit
- Understand local rules and safety

**Pain Points:**

- Unfamiliar with app and vehicle operation
- Language barriers (prefers English)
- Concerns about getting charged incorrectly

**AI Interaction:**

- Heavy reliance on conversational support for onboarding
- Needs clear, step-by-step guidance
- Low tolerance for AI errors (new user trust fragile)
- Appreciates transparency and citations

**Key Scenarios:**

- "How do I start a ride?"
- "Can I park the scooter here?" (shows location)
- "What are the helmet rules in Amsterdam?"

---

#### Persona: "Family Frank"

**Profile:**

- Age: 42, Father of 2
- Location: Paris suburbs
- Usage: Weekend trips with family
- Preferred vehicle: Electric van

**Goals:**

- Safe, spacious vehicle for family outings
- Transparent pricing (budget-conscious)
- Reliable vehicles (can't afford breakdowns with kids)

**Pain Points:**

- Higher costs for vans (price-sensitive)
- Need to verify vehicle cleanliness and safety before use
- Concerns about incidents with family aboard

**AI Interaction:**

- Uses conversational support for vehicle condition questions
- Values explainable pricing (why van costs more)
- Highly sensitive to safety—wants human oversight for critical issues
- Appreciates proactive maintenance notifications

**Key Scenarios:**

- "Is this van clean and suitable for kids?"
- "Why did the price increase by 20% this weekend?"
- "I noticed a weird noise—is the van safe to drive?"

---

### 2. Operations Team

Internal team managing fleet operations, customer support, and incidents.

#### Persona: "Operations Manager Olga"

**Profile:**

- Age: 34, Operations Manager
- Team: 8 support agents + 5 field technicians
- Location: Operations center, Munich
- Experience: 5 years in mobility operations

**Goals:**

- Reduce operational costs while maintaining service quality
- Fast incident resolution to minimize downtime
- Data-driven decisions for fleet management
- Maintain high customer satisfaction scores

**Pain Points:**

- **"Right vehicles not in right places"**: #1 customer complaint, difficult to solve manually
- **Reactive rebalancing**: Always responding to complaints, never ahead of demand
- **Battery management chaos**: Crews don't know which vehicles to prioritize for battery swaps
- **No demand visibility**: Can't predict where/when vehicles will be needed (weather, events, commute patterns)
- **Charge-out incidents**: Vehicles frequently run out of battery, customer complaints spike
- Overwhelmed by repetitive support tickets
- Slow incident investigation (manual data collection)
- Difficult to identify patterns across incidents
- Compliance documentation burden (EU AI Act)

**AI Interaction:**

- **Fleet Intelligence (Primary)**: Uses demand forecasts to plan vehicle distribution proactively
- **Rebalancing Optimization**: AI generates optimized crew routes for vehicle redistribution
- **Battery Management**: Prioritizes battery swap tasks based on AI predictions
- **Predictive Pre-Positioning**: Identifies regular commuters for guaranteed vehicle availability
- Uses AI incident summarization to triage faster
- Reviews HITL queue for high-risk AI decisions
- Relies on dashboards for GenAI performance metrics

**Key Scenarios:**

- "Show me demand forecast for tomorrow morning's commute—where do we need more eBikes?"
- "Generate rebalancing plan for field crews tonight based on predicted demand"
- "Which vehicles need battery swaps urgently? What's the optimal route?"
- "Identify regular commuters on Route A who would benefit from guaranteed vehicle availability"
- "Show me all incidents in Paris today, prioritized by severity"
- "Review this AI-flagged theft attempt—approve immobilization?"

---

#### Persona: "Field Technician Theo"

**Profile:**

- Age: 27, Field Technician & Battery Swap Specialist
- Team: Part of 5-person maintenance crew + 3-person battery swap crew
- Location: Mobile (covers downtown + suburbs)
- Experience: 2 years with MobilityCorp
- Equipment: Service van with spare batteries for scooters/eBikes

**Goals:**

- Efficiently locate and repair broken vehicles
- Optimize battery swap routes to maximize vehicles serviced
- Minimize vehicle downtime and charge-outs
- Clear instructions for issue resolution
- Fair work distribution

**Pain Points:**

- **Inefficient battery swap routes**: Manual route planning wastes time and fuel
- **Unclear prioritization**: Which vehicles need battery swaps most urgently?
- **Reactive mode**: Only swapping batteries after vehicles run out, not proactively
- **Wasted trips**: Arriving at vehicles that don't actually need swaps yet
- Incomplete incident reports (what's actually broken?)
- Wasted trips due to poor diagnostics
- Manual tracking of maintenance tasks

**AI Interaction:**

- **Battery Swap Optimization (Primary)**: Receives AI-generated priority list and optimized routes
- **Charge Prediction**: AI tells him which vehicles will run out soon (proactive swaps)
- Reads AI-generated incident summaries for context
- Relies on AI diagnosis for pre-trip preparation
- Benefits from AI-suggested similar past incidents
- Needs actionable information, not generic summaries

**Key Scenarios:**

- "Show me today's battery swap priority list—which vehicles need swaps urgently?"
- "Generate optimal route to swap batteries for 12 scooters in downtown area"
- "Which eBikes are predicted to run out of charge in the next 2 hours?"
- "Read incident report before driving to broken scooter"
- "See similar incidents—what fixed them?"
- "Vehicle marked as 'unusual battery drain'—what to check?"

---

### 3. System Administrators

Technical team responsible for platform infrastructure and operations.

#### Persona: "DevOps Engineer Dana"

**Profile:**

- Age: 31, Senior DevOps Engineer
- Team: 4-person DevOps team
- Location: Remote (distributed team)
- Experience: 8 years in cloud infrastructure

**Goals:**

- High system availability (99.9%+)
- Efficient incident response
- Cost-optimized infrastructure
- Secure and compliant operations

**Pain Points:**

- Complex microservices architecture to monitor
- GenAI Platform requires specialized GPU infrastructure
- Compliance requirements add operational overhead
- AI model updates risk introducing regressions

**AI Interaction:**

- Monitors GenAI Platform health metrics
- Manages TEVV pipeline and model deployments
- Investigates AI-related incidents
- Reviews audit logs for compliance

**Key Scenarios:**

- "GenAI Platform latency spiked—investigate"
- "Deploy new LLM model to shadow mode for testing"
- "Generate audit report for last 90 days of AI decisions"
- "Why did the HITL approval rate jump from 8% to 15%?"

---

### 4. Compliance & Legal Team

Ensures regulatory compliance, especially EU AI Act requirements.

#### Persona: "Compliance Officer Carmen"

**Profile:**

- Age: 39, Head of Compliance
- Team: 2 legal specialists + external counsel
- Location: Brussels (EU HQ)
- Experience: 12 years in regulatory compliance

**Goals:**

- Full EU AI Act compliance for high-risk AI system
- Audit-ready documentation at all times
- Risk mitigation for AI-related incidents
- Clear accountability for AI decisions

**Pain Points:**

- AI regulations are new and evolving
- Difficult to prove AI system safety and transparency
- Manual audit trail reviews are time-consuming
- Balancing innovation with compliance

**AI Interaction:**

- Reviews model cards and training data documentation
- Audits AI decision logs for high-risk scenarios
- Ensures HITL processes are followed
- Validates transparency and explainability features

**Key Scenarios:**

- "Prepare for EU AI Act compliance audit"
- "Review all high-risk AI decisions from last quarter"
- "Verify all GenAI responses include proper citations"
- "Ensure users can opt out of AI-driven personalization"

---

### 5. Business Stakeholders

Executive and product leadership driving business strategy.

#### Persona: "CPO Patricia"

**Profile:**

- Age: 44, Chief Product Officer
- Team: Product managers, designers, analysts
- Location: Amsterdam (HQ)
- Experience: 15 years in mobility and tech products

**Goals:**

- Drive user growth and retention
- Achieve cost savings targets (40% support cost reduction)
- Differentiate from competitors with AI
- Expand to new markets profitably

**Pain Points:**

- Unclear ROI on AI investments
- Risk of AI failures damaging brand reputation
- Balancing AI innovation with safety/compliance
- Difficulty measuring AI's business impact

**AI Interaction:**

- Reviews GenAI value proposition dashboards
- Monitors customer satisfaction with AI features
- Approves AI roadmap and budget
- Champions AI-first strategy internally

**Key Scenarios:**

- "What's the ROI on GenAI conversational support?"
- "Are customers satisfied with AI interactions?"
- "Can we expand AI to 5 new cities this year?"
- "What's our AI differentiation vs. competitors?"

---

## Secondary Actors

### 6. External Systems

**Payment Gateway (Stripe/similar)**

- Processes payments and refunds
- PCI-DSS compliant
- Interaction: API-based

**Map Services (Google Maps/similar)**

- Provides geocoding, routing, location services
- Interaction: API-based

**LLM Provider (OpenAI, Anthropic)**

- Provides foundational LLM capabilities
- Interaction: API-based, model versioning

**IoT Vehicles (Fleet)**

- Electric scooters, eBikes, cars, vans with embedded IoT
- Sends telemetry (location, battery, sensors)
- Receives commands (lock/unlock, diagnostics)
- Interaction: MQTT protocol

---

## Actor Interaction Summary

| Actor                | Primary Interactions                          | AI Touchpoints                                       |
| -------------------- | --------------------------------------------- | ---------------------------------------------------- |
| **Customers**        | Mobile app, support, bookings                 | Conversational support, personalized recommendations |
| **Operations Team**  | Dashboard, incident management, HITL approval | Incident summaries, anomaly explanations, HITL queue |
| **DevOps Team**      | Infrastructure monitoring, deployments        | GenAI Platform health, TEVV pipeline, audit logs     |
| **Compliance Team**  | Audit reports, model documentation            | Model cards, audit trails, HITL tracking             |
| **Business Team**    | Analytics dashboards, KPIs                    | AI ROI metrics, user satisfaction with AI            |
| **External Systems** | API integrations, IoT telemetry               | LLM API calls, payment processing, map services      |

---

## User Journey: AI-Powered Support Interaction

**Scenario**: Commuter Clara's eBike won't unlock

1. **Clara**: Opens app, taps "Help", types "My bike won't unlock"
2. **GenAI Platform**:
   - Retrieves relevant troubleshooting guides via RAG
   - Generates response with step-by-step instructions
   - Includes citations to help articles
   - Response time: 1.8 seconds
3. **Clara**: Follows steps (restart app, check Bluetooth)
4. **GenAI Platform**: Asks "Did this solve your issue?"
5. **Clara**: "Still not working"
6. **GenAI Platform**:
   - Escalates to human support (automatic ticket creation)
   - Notifies operations team
   - Provides context from conversation
7. **Operations Team**: Unlocks bike remotely + schedules maintenance check
8. **Clara**: Bike unlocks, rides successfully
9. **Audit Store**: Logs entire interaction for compliance and quality review

**Result**: Issue resolved in <3 minutes with hybrid AI + human approach, full audit trail maintained.
