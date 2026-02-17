# Lab M3.01 - Create VPC with Public and Private Subnets

## Overview
This lab demonstrates how to create a production-ready AWS VPC with proper network segmentation.
The VPC includes public and private subnets distributed across multiple Availability Zones,
with routing configured to allow internet access only for public subnets.

---

## Network Design

### VPC CIDR
- VPC CIDR block: 10.0.0.0/16

### Subnet Allocation

**Public Subnets**
- eu-central-1a: 10.0.1.0/24
- eu-central-1b: 10.0.2.0/24

**Private Subnets**
- eu-central-1a: 10.0.11.0/24
- eu-central-1b: 10.0.12.0/24

Reserved IP ranges were left available for future expansion.

---

## Architecture Description
- A custom VPC was created with DNS hostnames enabled.
- An Internet Gateway was attached to the VPC.
- Public subnets are associated with a route table that routes 0.0.0.0/0 traffic to the Internet Gateway.
- Private subnets are associated with a route table that contains only the local route, keeping them isolated.
- Subnets are distributed across two Availability Zones for high availability.

---

## Step-by-Step Process

1. Created a custom VPC with CIDR 10.0.0.0/16.
2. Enabled DNS hostnames for the VPC.
3. Created and attached an Internet Gateway.
4. Created two public and two private subnets across two Availability Zones.
5. Enabled auto-assign public IPs for public subnets.
6. Created separate route tables for public and private traffic.
7. Associated public subnets with the public route table.
8. Associated private subnets with the private route table.

---

## Validation and Testing
Connectivity was validated by checking route tables and subnet associations.
Public subnets have direct internet access through the Internet Gateway.
Private subnets do not have a route to the Internet Gateway and remain isolated.

Detailed validation steps are documented in the validation folder.

---

## Reflection Questions

**Why use 10.0.0.0/16 instead of 10.0.0.0/24?**  
Using a /16 provides significantly more IP space, allowing future growth and additional subnets without recreating the VPC.

**What is the difference between public and private subnets?**  
Public subnets have a route to an Internet Gateway, while private subnets do not.

**Why deploy across multiple Availability Zones?**  
To improve fault tolerance and availability in case one Availability Zone fails.

**How many usable IP addresses are in a /24 subnet?**  
Each /24 subnet has 256 total IPs, with 251 usable addresses after AWS reserves 5.

**Can additional subnets be added later?**  
Yes. The unused address space within the VPC CIDR allows for future subnet creation.
