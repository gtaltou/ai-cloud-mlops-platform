```mermaid
flowchart TB

    Internet["Internet"]

    IGW["Internet Gateway"]

    subgraph VPC["VPC 10.0.0.0/16"]

        subgraph Public["Public Subnets"]

            RT_PUBLIC["RT Public"]

            ALB["ALB"]

            NAT["NAT Gateway"]
        end

        subgraph App["Private App Subnets"]

            RT_APP["RT App"]

            EKS["EKS"]

            API["FastAPI"]

            AGENT["Agents"]

            RAG["RAG"]
        end

        subgraph Data["Private Data Subnets"]

            RT_DATA["RT Data"]

            Aurora["Aurora"]

            Redis["Redis"]

            OpenSearch["OpenSearch"]
        end

        subgraph Endpoints["PrivateLink"]

            BedrockEP["Bedrock"]

            SecretsEP["Secrets"]

            STSEP["STS"]

            KMSEP["KMS"]

            CloudWatchEP["CloudWatch"]

            S3EP["S3"]
        end

    end

    Internet --> IGW

    IGW --> ALB

    ALB --> EKS

    EKS --> Aurora
    EKS --> Redis
    EKS --> OpenSearch

    EKS --> BedrockEP
    EKS --> SecretsEP
    EKS --> STSEP
    EKS --> KMSEP
    EKS --> CloudWatchEP
    EKS --> S3EP
```


# Security Zone Matrix

| Zone | Internet Accessible | Description |
|--------|--------|--------|
| Edge | Yes | CloudFront, WAF |
| Public | Yes | Load Balancers |
| Application | No | FastAPI, Agents, RAG, MCP |
| Data | No | Aurora, Redis, OpenSearch |
| Management | No | Monitoring and Administration |
| PrivateLink | No | AWS Service Endpoints |