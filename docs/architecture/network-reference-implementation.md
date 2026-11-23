# Network Terraform Reference Implementation

This document provides the reference Terraform implementation for the platform network architecture.

---

# Architecture Summary

## VPC

```text
10.0.0.0/16
```

## Availability Zones

```text
eu-west-1a
eu-west-1b
```

## Public Subnets

```text
10.0.1.0/24
10.0.2.0/24
```

## Private Application Subnets

```text
10.0.11.0/24
10.0.12.0/24
```

## Private Data Subnets

```text
10.0.21.0/24
10.0.22.0/24
```

---

# Terraform Architecture

```text
network/
├── main.tf
├── variables.tf
├── outputs.tf
├── vpc.tf
├── subnets.tf
├── routes.tf
├── nat.tf
├── endpoints.tf
├── security-groups.tf
└── flowlogs.tf
```

---

# VPC

## vpc.tf

```hcl
resource "aws_vpc" "main" {

  cidr_block           = "10.0.0.0/16"

  enable_dns_support   = true

  enable_dns_hostnames = true

  tags = {
    Name = "ai-platform-vpc"
  }
}
```

---

# Internet Gateway

```hcl
resource "aws_internet_gateway" "igw" {

  vpc_id = aws_vpc.main.id

  tags = {
    Name = "ai-platform-igw"
  }
}
```

---

# Public Subnets

```hcl
resource "aws_subnet" "public_a" {

  vpc_id            = aws_vpc.main.id

  cidr_block        = "10.0.1.0/24"

  availability_zone = "eu-west-1a"

  map_public_ip_on_launch = true
}

resource "aws_subnet" "public_b" {

  vpc_id            = aws_vpc.main.id

  cidr_block        = "10.0.2.0/24"

  availability_zone = "eu-west-1b"

  map_public_ip_on_launch = true
}
```

---

# Application Subnets

```hcl
resource "aws_subnet" "app_a" {

  vpc_id            = aws_vpc.main.id

  cidr_block        = "10.0.11.0/24"

  availability_zone = "eu-west-1a"
}

resource "aws_subnet" "app_b" {

  vpc_id            = aws_vpc.main.id

  cidr_block        = "10.0.12.0/24"

  availability_zone = "eu-west-1b"
}
```

---

# Data Subnets

```hcl
resource "aws_subnet" "data_a" {

  vpc_id            = aws_vpc.main.id

  cidr_block        = "10.0.21.0/24"

  availability_zone = "eu-west-1a"
}

resource "aws_subnet" "data_b" {

  vpc_id            = aws_vpc.main.id

  cidr_block        = "10.0.22.0/24"

  availability_zone = "eu-west-1b"
}
```

---

# Elastic IPs

```hcl
resource "aws_eip" "nat_a" {

  domain = "vpc"
}

resource "aws_eip" "nat_b" {

  domain = "vpc"
}
```

---

# NAT Gateways

```hcl
resource "aws_nat_gateway" "nat_a" {

  allocation_id = aws_eip.nat_a.id

  subnet_id     = aws_subnet.public_a.id
}

resource "aws_nat_gateway" "nat_b" {

  allocation_id = aws_eip.nat_b.id

  subnet_id = aws_subnet.public_b.id
}
```

---

# Public Route Table

```hcl
resource "aws_route_table" "public" {

  vpc_id = aws_vpc.main.id

  route {

    cidr_block = "0.0.0.0/0"

    gateway_id = aws_internet_gateway.igw.id
  }
}
```

---

# Private Route Table

```hcl
resource "aws_route_table" "private_a" {

  vpc_id = aws_vpc.main.id

  route {

    cidr_block = "0.0.0.0/0"

    nat_gateway_id = aws_nat_gateway.nat_a.id
  }
}
```

---

# S3 Gateway Endpoint

```hcl
resource "aws_vpc_endpoint" "s3" {

  vpc_id = aws_vpc.main.id

  service_name = "com.amazonaws.eu-west-1.s3"

  route_table_ids = [
    aws_route_table.private_a.id
  ]

  vpc_endpoint_type = "Gateway"
}
```

---

# Bedrock Endpoint

```hcl
resource "aws_vpc_endpoint" "bedrock" {

  vpc_id = aws_vpc.main.id

  service_name =
    "com.amazonaws.eu-west-1.bedrock-runtime"

  vpc_endpoint_type = "Interface"

  subnet_ids = [

    aws_subnet.app_a.id,

    aws_subnet.app_b.id
  ]

  private_dns_enabled = true
}
```

---

# Secrets Manager Endpoint

```hcl
resource "aws_vpc_endpoint" "secretsmanager" {

  vpc_id = aws_vpc.main.id

  service_name =
    "com.amazonaws.eu-west-1.secretsmanager"

  vpc_endpoint_type = "Interface"

  subnet_ids = [

    aws_subnet.app_a.id,

    aws_subnet.app_b.id
  ]

  private_dns_enabled = true
}
```

---

# KMS Endpoint

```hcl
resource "aws_vpc_endpoint" "kms" {

  vpc_id = aws_vpc.main.id

  service_name =
    "com.amazonaws.eu-west-1.kms"

  vpc_endpoint_type = "Interface"

  subnet_ids = [

    aws_subnet.app_a.id,

    aws_subnet.app_b.id
  ]
}
```

---

# CloudWatch Endpoint

```hcl
resource "aws_vpc_endpoint" "logs" {

  service_name =
    "com.amazonaws.eu-west-1.logs"

  vpc_id = aws_vpc.main.id

  subnet_ids = [

    aws_subnet.app_a.id,

    aws_subnet.app_b.id
  ]

  vpc_endpoint_type = "Interface"
}
```

---

# STS Endpoint

```hcl
resource "aws_vpc_endpoint" "sts" {

  service_name =
    "com.amazonaws.eu-west-1.sts"

  vpc_id = aws_vpc.main.id

  subnet_ids = [

    aws_subnet.app_a.id,

    aws_subnet.app_b.id
  ]

  vpc_endpoint_type = "Interface"
}
```

---

# VPC Flow Logs

```hcl
resource "aws_flow_log" "vpc" {

  traffic_type = "ALL"

  vpc_id = aws_vpc.main.id

  log_destination_type = "cloud-watch-logs"
}
```

---

# Security Groups

## Application Tier

Allowed:

```text
443 from ALB
```

Outbound:

```text
443
5432
6379
```

---

## Data Tier

Allowed:

```text
5432 TCP
6379 TCP
443 HTTPS
```

Only from application subnets.

---

# Outputs

```hcl
output "vpc_id" {

  value = aws_vpc.main.id
}

output "public_subnets" {

  value = [
    aws_subnet.public_a.id,
    aws_subnet.public_b.id
  ]
}

output "private_app_subnets" {

  value = [
    aws_subnet.app_a.id,
    aws_subnet.app_b.id
  ]
}

output "private_data_subnets" {

  value = [
    aws_subnet.data_a.id,
    aws_subnet.data_b.id
  ]
}
```

---

# Future Enhancements

- Transit Gateway
- Multi-Account Networking
- Shared Services VPC
- AWS Cloud WAN
- IPv6
- Direct Connect
- Site-to-Site VPN
- Azure Interconnect
- Google Cloud Interconnect
- Multi-Region Failover