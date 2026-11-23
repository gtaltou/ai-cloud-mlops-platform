## Cloud Strategy Overview

```mermaid
flowchart TB

    Users["Users"]

    Vercel["Vercel"]

    AWS["AWS Primary Platform"]

    Azure["Azure Secondary Platform"]

    GCP["GCP Secondary Platform"]

    Users --> Vercel

    Vercel --> AWS

    AWS -. Optional .-> Azure

    AWS -. Optional .-> GCP
```

## AWS Reference Architecture

```mermaid
flowchart TB

    Internet["Internet"]

    CloudFront["CloudFront"]

    AppRunner["App Runner"]

    FastAPI["FastAPI Platform"]

    Bedrock["AWS Bedrock"]

    Lambda["Lambda"]

    Aurora["Aurora Serverless"]

    Redis["Redis Cache"]

    S3["Amazon S3"]

    VectorDB["Vector Database"]

    Internet --> CloudFront

    CloudFront --> AppRunner

    AppRunner --> FastAPI

    FastAPI --> Bedrock

    FastAPI --> Lambda

    FastAPI --> Aurora

    FastAPI --> Redis

    FastAPI --> S3

    FastAPI --> VectorDB
```


## Network Architecture

```mermaid
flowchart TB

    Internet["Internet"]

    CloudFront["CloudFront"]

    Public["Public Services"]

    Private["Private Services"]

    Data["Data Services"]

    Internet --> CloudFront

    CloudFront --> Public

    Public --> Private

    Private --> Data
```


## AI Platform Architecture

```mermaid
flowchart LR

    API["Application API"]

    AgentPlatform["Agent Platform"]

    MCP["MCP Gateway"]

    RAG["RAG Platform"]

    Gateway["Model Gateway"]

    Bedrock["AWS Bedrock"]

    OpenAI["OpenAI"]

    Claude["Claude"]

    API --> AgentPlatform

    AgentPlatform --> MCP

    AgentPlatform --> RAG

    AgentPlatform --> Gateway

    Gateway --> Bedrock

    Gateway --> OpenAI

    Gateway --> Claude
```


## Environment Strategy

```mermaid
flowchart LR

    Developer["Developer"]

    Dev["Development"]

    Staging["Staging"]

    Prod["Production"]

    Developer --> Dev

    Dev --> Staging

    Staging --> Prod
```


## Deployment Pipeline

```mermaid
flowchart LR

    GitHub["GitHub"]

    CI["CI"]

    Validation["Quality Gates"]

    Dev["Dev"]

    Staging["Staging"]

    Prod["Production"]

    GitHub --> CI

    CI --> Validation

    Validation --> Dev

    Dev --> Staging

    Staging --> Prod
```


## Resilience Architecture

```mermaid
flowchart TB

    Users["Users"]

    CloudFront["CloudFront"]

    AppRunner["App Runner"]

    Lambda["Lambda"]

    Aurora["Aurora"]

    Backup["Backups"]

    Users --> CloudFront

    CloudFront --> AppRunner

    AppRunner --> Lambda

    AppRunner --> Aurora

    Aurora --> Backup
```


## Cost Governance

```mermaid
flowchart LR

    Services["Cloud Services"]

    Metrics["Usage Metrics"]

    FinOps["FinOps Dashboard"]

    Alerts["Budget Alerts"]

    Services --> Metrics

    Metrics --> FinOps

    FinOps --> Alerts
```


