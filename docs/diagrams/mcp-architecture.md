# MCP Architecture

```mermaid
flowchart TB

    Agent

    Agent --> MCPGateway

    MCPGateway --> GitHubMCP

    MCPGateway --> FilesystemMCP

    MCPGateway --> DatabaseMCP

    MCPGateway --> CloudMCP

    CloudMCP --> AWS

    CloudMCP --> Azure

    CloudMCP --> GCP

    DatabaseMCP --> PostgreSQL

    DatabaseMCP --> Redis
```