# Secure Ingress & Egress for a Core Application VPC  
**Inspection VPC Pattern using AWS Transit Gateway & Network Firewall**

---

## 1. Overview

This repository contains a Terraform-based implementation of a **secure, isolated network architecture** for a critical application deployed in **us-east-1**.

The design follows an **Inspection VPC (DMZ) pattern**, where **all ingress and egress traffic** to the application is **forced through centralized inspection controls** before reaching the internet or the application VPC.

This pattern is commonly used in security-sensitive, compliance-driven environments to enforce:
- Centralized traffic inspection
- No direct internet access from application workloads
- Clear separation of responsibilities between networking and application teams

---

## 2. High-Level Architecture

### VPCs

| VPC | CIDR | Purpose |
|---|---|---|
| **AppVPC** | `10.10.0.0/16` | Hosts the application workloads (private only, no IGW) |
| **InspectionVPC** | `10.20.0.0/16` | DMZ VPC for ingress/egress inspection |

### Core AWS Components
- AWS Transit Gateway (TGW)
- AWS Network Firewall
- NAT Gateways
- Internet Gateway (InspectionVPC only)

---

## 3. Architecture Diagram

Internet
                        |
                        |
                +----------------+
                |  Internet GW   |
                +----------------+
                        |
              Public Subnets (InspectionVPC)
                        |
                +----------------+
                |  Public ALB    |
                +----------------+
                        |
                +----------------+
                | Network Firewall|
                |  Endpoints     |
                +----------------+
                        |
                +----------------+
                |  Transit GW    |
                +----------------+
                   /          \
                  /            \
     AppVPC Attachment      InspectionVPC Attachment
            |                      |
    Private Subnets            NAT Subnets
            |                      |
    +----------------+      +----------------+
    | Internal ALB / |      |  NAT Gateway   |
    | App Workloads  |      +----------------+
    +----------------+              |
                                     |
                                  Internet

# Terraform setup
1. Setup AWS account
2. Install terraform latest version
3. install AWS CLI in the machine
4. Get access key , secret key, region and Account ID of the AWS Account

# Run The code 
`cd assignment`
`ls` --> it will list all the files in assignment folder
# Run Terraform commands 
`terraform init`
`terraform plan`
`terraform apply`