# Predictive Fleet Positioning

Allowing purely on "natural" (usage-driven) distribution of the fleet is suboptimal, because small spikes, like popular
events, peak hours, etc., can lead to poor service levels. Predictive fleet positioning aims to anticipate demand and
position vehicles accordingly.

The following aspects are considered for positioning decisions:

- Current demand and short-term prediction based on statistical models
- Historical demand patterns (time of day, day of week, day of the year, repetitive events, such as holidays, etc.)
- Real-time events (e.g., concerts, sports events) that may influence demand
- External factors (e.g., weather conditions, public transport disruptions, social situation)

Fleet repositioning has the following goals:

- Supply the demand, reducing customer wait times
- Optimize fleet utilization, reducing idle times and increasing revenue
- Preserving fleet from damages in case of expected adverse weather conditions or harsh social events, such as protests,
  football matches, etc.

## How it works

1. Current fleet state and positioning is collected, aggregated by a **streaming data platform**.
2. Weather condition is periodically collected by a dedicated microservice.
3. Social and entertainment events are collected from external sources by a dedicated scraping microservice. Data is analyzed using LLMs to extract potential impact on demand. Structured data is stored in a database and served to a prediction model.
4. A **prediction engine** (microservice) combines all the data and generates positioning recommendations using a deterministic statistical models.
5. Recommendations are sent to a **fleet management microservice**, which translates them into concrete repositioning tasks for vehicles and drivers.

The following diagram illustrates the cooperation between components:

```mermaid
graph TB
    %% External Systems
    WeatherAPI[Weather API]
    EventFeeds[Event Sources<br/>City/Ticketing/Social]
    Fleet[Fleet Vehicles<br/>IoT Devices]

    %% Actors
    OpsTeam[Operations Team<br/>Ops Dashboard]
    FieldCrew[Field Crew<br/>Drivers]
    
    %% AI
    EventsAgent[Events Analysing Agent<br/>GenAI + NLP]

    %% Streaming
    TelemetryPipeline[Telemetry Pipeline<br/>MQTT + TimescaleDB]
    DemandPipeline[Demand Pipeline<br/>MQTT + TimescaleDB]

    %% Infra
    EventBus[Event Bus<br/>Apache Kafka]

    %% Predictive Positioning Bounded Context
    subgraph "Predictive Positioning (Bounded Context)"
        Weather[Weather Service]
        WeatherDB[(Wheather DB)]
        
        EventIntel[Event Intelligence Service]
        EventsDB[(Events DB)]
        
        DemandForecast[Demand Forecasting Service]
        DemandHistoryDB[(Demand History DB)]

        FleetPosDB[(Fleet Position & State DB)]
        
        PositionOptimizer[Repositioning Optimizer]
        PredDB[(Predictions DB)]
    end

    %% Core Services
    subgraph "Core Services"
        BookingService[Booking Service]
        FleetService[Fleet Service]
    end

    Weather -->|Collect & Aggregate| WeatherAPI
    Weather --> WeatherDB

    EventIntel -->|Collect| EventFeeds
    EventIntel -->|Analyze| EventsAgent
    EventIntel --> EventsDB

    DemandHistoryDB --> DemandForecast

    WeatherDB --> PositionOptimizer
    EventsDB --> PositionOptimizer
    DemandForecast --> PositionOptimizer
    FleetPosDB --> PositionOptimizer

    PositionOptimizer -->|Store| PredDB
    PositionOptimizer --> |Publish repositioning-plan.*| EventBus

    TelemetryPipeline -->|Aggregate| FleetPosDB
    DemandPipeline -->|Aggregate| DemandHistoryDB

    BookingService -->|Publish booking.* and search.*| EventBus
    FleetService -->|Publish vehicle.status.*| EventBus

    Fleet -->|Telemetry| TelemetryPipeline
    EventBus -->|vehicle.status.*| TelemetryPipeline
    EventBus -->|booking.* and search.*| DemandPipeline

    EventBus -->|Consume repositioning-plan.*| FleetService

    %% Human oversight & execution
    OpsTeam -->|Approve/override plans| PositionOptimizer
    APIGateway --> PositionOptimizer
    OpsTeam -->|Dispatch & monitor| APIGateway
    APIGateway --> FleetService
    FleetService -->|Assignments & routes| FieldCrew

    style EventBus fill:#E74C3C
    
    style WeatherDB fill:#9B59B6
    style EventsDB fill:#9B59B6
    style PredDB fill:#9B59B6
    style DemandHistoryDB fill:#9B59B6
    style FleetPosDB fill:#9B59B6

    style APIGateway fill:#F39C12

    style PositionOptimizer fill:#4A90E2
    style FleetService fill:#4A90E2
    style BookingService fill:#4A90E2
    style Weather fill:#4A90E2
    style EventIntel fill:#4A90E2
    style DemandForecast fill:#4A90E2

    style TelemetryPipeline fill:#95A5A6
    style DemandPipeline fill:#95A5A6
    
    style OpsTeam fill:#50C878
    style FieldCrew fill:#50C878
```