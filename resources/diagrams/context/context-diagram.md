# Context Diagram - MobilityCorp System

## Description

This diagram shows the MobilityCorp vehicle-sharing platform in its external context, including all external actors and systems that interact with it. MobilityCorp supports electric scooters, eBikes, electric cars, and vans.

## Actors & External Systems

- **Customers**: Use mobile app to find, book, and use vehicles
- **Operations Team**: Manage fleet, handle incidents, monitor system health
- **Vehicles**: IoT-enabled electric scooters, eBikes, cars, and vans sending telemetry
- **Payment Gateway**: External payment processing (Stripe/similar)
- **Map Services**: External mapping and routing (Google Maps/similar)
- **AI/ML Platform**: External LLM provider for GenAI capabilities

## Diagram

```mermaid
C4Context
    title Context Diagram - MobilityCorp Vehicle-Sharing Platform

    Person(customer, "Customer", "Uses mobile app to find, book, and ride vehicles")
    Person(ops_team, "Operations Team", "Manages fleet, handles incidents, monitors operations")

    System(mobility_system, "MobilityCorp Platform", "Vehicle-sharing platform with AI-powered operations for e-scooters, eBikes, electric cars & vans")

    System_Ext(vehicles, "Fleet Vehicles", "Electric scooters, eBikes, cars & vans with IoT sensors and telemetry")
    System_Ext(payment, "Payment Gateway", "Processes payments and refunds (Stripe/similar)")
    System_Ext(maps, "Map Services", "Provides mapping, routing, and location services")
    System_Ext(llm_provider, "AI/ML Platform", "External LLM provider for GenAI Platforms")

    Rel(customer, mobility_system, "Books vehicles, views trips, requests support", "HTTPS/Mobile App")
    Rel(ops_team, mobility_system, "Manages fleet, reviews incidents, monitors operations", "HTTPS/Web Dashboard")

    Rel(mobility_system, vehicles, "Sends commands (lock/unlock), receives telemetry", "MQTT/IoT")
    Rel(mobility_system, payment, "Processes payments", "HTTPS/API")
    Rel(mobility_system, maps, "Gets locations, routes", "HTTPS/API")
    Rel(mobility_system, llm_provider, "Sends prompts, receives AI responses", "HTTPS/API")

    UpdateRelStyle(customer, mobility_system, $offsetY="-40", $offsetX="-50")
    UpdateRelStyle(ops_team, mobility_system, $offsetY="-40", $offsetX="50")
```

## Key Interactions

1. **Customer Journey**: Customers interact with the mobile app to find nearby vehicles, make bookings, unlock vehicles, and request support
2. **Operations**: Operations team uses web dashboard to manage fleet distribution, respond to incidents, and monitor system health
3. **Vehicle Telemetry**: Vehicles continuously send location, battery status, and sensor data to the platform
4. **Payment Processing**: All financial transactions are handled through external payment gateway
5. **AI Enhancement**: GenAI capabilities are provided through integration with external LLM platform, used for conversational support, incident summarization, and anomaly explanation

## References

- See [Container Diagram](../container/container-diagram.md) for internal system structure
- See [ADR-002](../../../Architecture-Decision-Records/002-microservices-architecture) for architecture style decision
