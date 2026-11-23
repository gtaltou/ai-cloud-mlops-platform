# End-to-End Data Flow

```mermaid
sequenceDiagram

    actor User

    participant Frontend

    participant Backend

    participant Agent

    participant RAG

    participant LLM

    User->>Frontend: Submit Request

    Frontend->>Backend: API Call

    Backend->>Agent: Route Request

    Agent->>RAG: Retrieve Context

    RAG-->>Agent: Relevant Context

    Agent->>LLM: Prompt + Context

    LLM-->>Agent: Response

    Agent-->>Backend: Final Result

    Backend-->>Frontend: API Response

    Frontend-->>User: Render Output
```