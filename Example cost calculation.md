# WebSocket Service Infrastructure

This document outlines the infrastructure setup and calculations for a WebSocket service handling 1M daily connections.

## Traffic Distribution

Daily traffic pattern for 1M connections:
- **Peak Hours (4 hours)**: 70% of traffic (~175,000 connections/hour)
- **Normal Hours (12 hours)**: 20% of traffic (~16,700 connections/hour)
- **Night Hours (8 hours)**: 10% of traffic (~12,500 connections/hour)

## Infrastructure Setup

### ECS EC2 Configuration

We use ECS EC2 instead of Fargate for better control over WebSocket connections and cost optimization.

#### Base Configuration (24/7)
- Instance Type: t3.medium (4 vCPU, 4GB RAM)
- Quantity: 1
- Monthly Hours: 730 (100% utilization)
- Purpose: Handling night load and base traffic

#### Normal Hours Configuration (12h/day)
- Instance Type: t3.medium
- Quantity: 2
- Monthly Hours: 365 (50% utilization)
- Purpose: Handling medium traffic

#### Peak Hours Configuration (4h/day)
- Instance Type: t3.medium
- Quantity: 6
- Monthly Hours: 122 (16.67% utilization)
- Purpose: Handling peak traffic

### Load Balancer Setup
- Application Load Balancer (ALB)
- Sticky Sessions enabled
- Health checks configured

[Example of cost calculation](https://calculator.aws/#/estimate?id=385743ba2bdfc45cb209e86256525aef6fa2a45e)
