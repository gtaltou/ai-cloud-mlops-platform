# Azure Reference Architecture

## Purpose

Reference deployment architecture on Microsoft Azure.

---

## Azure AI Platform

```mermaid
flowchart TB

    Internet["Internet"]

    FrontDoor["Azure Front Door"]

    AppService["Azure App Service"]

    FastAPI["FastAPI Platform"]

    AzureOpenAI["Azure OpenAI"]

    Functions["Azure Functions"]

    PostgreSQL["Azure PostgreSQL"]

    Redis["Azure Cache for Redis"]

    Blob["Azure Blob Storage"]

    AISearch["Azure AI Search"]

    Internet --> FrontDoor

    FrontDoor --> AppService

    AppService --> FastAPI

    FastAPI --> AzureOpenAI

    FastAPI --> Functions

    FastAPI --> PostgreSQL

    FastAPI --> Redis

    FastAPI --> Blob

    FastAPI --> AISearch
```

---

## Azure Service Mapping

| Platform Capability | Azure Service |
|--------------------|---------------|
| CDN | Azure Front Door |
| Application Hosting | Azure App Service |
| Serverless | Azure Functions |
| Relational Database | Azure PostgreSQL |
| Object Storage | Azure Blob Storage |
| Cache | Azure Redis Cache |
| Vector Search | Azure AI Search |
| Foundation Models | Azure OpenAI |
| Secrets Management | Azure Key Vault |
| Monitoring | Azure Monitor |

---

## Azure AI Architecture

```mermaid
flowchart LR

    Agents["Agent Platform"]

    RAG["RAG Platform"]

    MCP["MCP Gateway"]

    Gateway["Model Gateway"]

    AzureOpenAI["Azure OpenAI"]

    AISearch["Azure AI Search"]

    Agents --> MCP

    Agents --> RAG

    Agents --> Gateway

    RAG --> AISearch

    Gateway --> AzureOpenAI
```

# GCP Reference Architecture

## Purpose

Reference deployment architecture on Google Cloud Platform.

---

## GCP AI Platform

```mermaid
flowchart TB

    Internet["Internet"]

    LB["Cloud Load Balancer"]

    CloudRun["Cloud Run"]

    FastAPI["FastAPI Platform"]

    VertexAI["Vertex AI"]

    Functions["Cloud Functions"]

    CloudSQL["Cloud SQL"]

    Memorystore["Memorystore Redis"]

    GCS["Cloud Storage"]

    VectorSearch["Vertex AI Vector Search"]

    Internet --> LB

    LB --> CloudRun

    CloudRun --> FastAPI

    FastAPI --> VertexAI

    FastAPI --> Functions

    FastAPI --> CloudSQL

    FastAPI --> Memorystore

    FastAPI --> GCS

    FastAPI --> VectorSearch
```

---

## GCP Service Mapping

| Platform Capability | GCP Service |
|--------------------|-------------|
| Load Balancer | Cloud Load Balancer |
| Application Hosting | Cloud Run |
| Serverless | Cloud Functions |
| Relational Database | Cloud SQL |
| Object Storage | Cloud Storage |
| Cache | Memorystore |
| Vector Search | Vertex AI Vector Search |
| Foundation Models | Vertex AI |
| Secrets | Secret Manager |
| Monitoring | Cloud Operations |

---

## GCP AI Architecture

```mermaid
flowchart LR

    Agents["Agent Platform"]

    RAG["RAG Platform"]

    MCP["MCP Gateway"]

    Gateway["Model Gateway"]

    VertexAI["Vertex AI"]

    VectorSearch["Vertex AI Vector Search"]

    Agents --> MCP

    Agents --> RAG

    Agents --> Gateway

    RAG --> VectorSearch

    Gateway --> VertexAI
```

## Multi-Cloud Service Mapping

| Capability | AWS | Azure | GCP |
|------------|-----|--------|-----|
| Frontend Hosting | Vercel | Static Web Apps | Firebase Hosting |
| API Hosting | App Runner | App Service | Cloud Run |
| Serverless | Lambda | Functions | Cloud Functions |
| Object Storage | S3 | Blob Storage | Cloud Storage |
| Database | Aurora | PostgreSQL | Cloud SQL |
| Cache | Redis | Azure Redis | Memorystore |
| Foundation Models | Bedrock | Azure OpenAI | Vertex AI |
| Vector Search | OpenSearch / Vector DB | AI Search | Vertex AI Search |
| Secrets | Secrets Manager | Key Vault | Secret Manager |
| Monitoring | CloudWatch | Azure Monitor | Cloud Operations |
| Infrastructure as Code | Terraform | Terraform | Terraform |



## Multi-Cloud Enterprise Architecture

```mermaid
flowchart TB

    Users["Users"]

    Frontend["Vercel / Frontend"]

    Platform["Application Platform"]

    AWS["AWS"]

    Azure["Azure"]

    GCP["GCP"]

    Users --> Frontend

    Frontend --> Platform

    Platform --> AWS

    Platform --> Azure

    Platform --> GCP
```


## Cloud Abstraction Strategy

```mermaid
flowchart TB

    Application["Application Layer"]

    Gateway["Platform Abstraction Layer"]

    AWS["AWS Services"]

    Azure["Azure Services"]

    GCP["GCP Services"]

    Application --> Gateway

    Gateway --> AWS

    Gateway --> Azure

    Gateway --> GCP
```


