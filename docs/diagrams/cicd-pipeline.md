# CI/CD Pipeline

```mermaid
flowchart LR

    Developer

    Developer --> GitHub

    GitHub --> Lint

    Lint --> Tests

    Tests --> SecurityScan

    SecurityScan --> Build

    Build --> TerraformPlan

    TerraformPlan --> Dev

    Dev --> Staging

    Staging --> Production
```