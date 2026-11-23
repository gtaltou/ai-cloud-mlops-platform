# Multi-Agent Architecture

```mermaid
flowchart TB

    User

    User --> Planner

    Planner --> Orchestrator

    Orchestrator --> ResearchAgent

    Orchestrator --> SecurityAgent

    Orchestrator --> FinanceAgent

    Orchestrator --> HealthcareAgent

    ResearchAgent --> Evaluator

    SecurityAgent --> Evaluator

    FinanceAgent --> Evaluator

    HealthcareAgent --> Evaluator

    Evaluator --> FinalResponse

    FinalResponse --> User
```