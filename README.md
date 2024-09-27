# Azure-Network-Security-DNS-Setup
# Azure Network and Security Configuration

## Overview
This project demonstrates the creation and configuration of virtual networks, security groups, and DNS zones on Azure. It includes the following tasks:
- Virtual network and subnet creation using the portal and templates
- Configuring Application Security Groups and Network Security Groups
- Public and private Azure DNS zones setup

## Task Breakdown
### 1. Virtual Networks
- **CoreServicesVnet**: Created via the Azure portal with custom subnets.
- **ManufacturingVnet**: Created via template.

### 2. Security Groups
- **Application Security Group** (asg-web): Allows web traffic.
- **Network Security Group** (myNSG): Configured to block internet traffic.

### 3. DNS Zones
- Public DNS for resolving hostnames.
- Private DNS linked to virtual networks.

## Files
- `CoreServicesVnet-template.json`: JSON template for CoreServicesVnet.
- `ManufacturingVnet-template.json`: Modified template for ManufacturingVnet.
