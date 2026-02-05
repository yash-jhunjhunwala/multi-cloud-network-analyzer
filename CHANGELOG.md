# Changelog

All notable changes to Multi-Cloud Network Analyzer will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-02-05

### 🎉 Initial Release

This is the first public release of the Multi-Cloud Network Analyzer - a production-ready tool for analyzing network infrastructure across AWS, Azure, and GCP.

### Features

#### Multi-Cloud Support
- **AWS** - VPCs, subnets, security groups, route tables, NAT gateways, Internet gateways
- **Azure** - VNets, subnets, NSGs, route tables, NAT gateways, public IPs
- **GCP** - VPCs, subnets, firewall rules, Cloud NAT, external IPs

#### Organization-Wide Scanning
- **AWS Organizations** - Scan all accounts with cross-account role assumption
- **Azure Tenants** - Scan all subscriptions in a tenant
- **GCP Organizations** - Scan all projects in an organization

#### Network Connectivity Detection
- **VPC/VNet Peering** - Detect peered networks across accounts/subscriptions/projects
- **Transit Gateway** - AWS Transit Gateway attachment detection
- **Internet Access** - Detect NAT gateways, Internet gateways, public IPs, Cloud NAT

#### Smart Recommendations
- **Optimal Deployment Location** - Best single location for maximum VM coverage
- **Full Coverage Plan** - Minimum set of deployments for 100% coverage (greedy set cover algorithm)
- **Unreachable Instances** - Detailed list of VMs that cannot be reached and why

#### Output & Reporting
- **JSON** - Machine-readable output for automation
- **CSV** - Spreadsheet-compatible format
- **HTML** - Rich D3.js network topology visualization
- **Summary** - Human-readable text summary

#### Performance & Reliability
- **Parallel Discovery** - Multi-threaded scanning (configurable parallelism)
- **Progress Tracking** - Real-time progress with ETA estimates
- **Caching** - Cache discovery results to speed up re-runs
- **Resumable Scans** - Resume interrupted organization scans

#### Cloud-Specific Modes

| Cloud | Single Mode | Organization Mode |
|-------|-------------|-------------------|
| AWS | `--mode account` | `--mode org` |
| Azure | `--mode subscription` | `--mode tenant` |
| GCP | `--mode project` | `--mode org` |

### Required Permissions

#### AWS
- `sts:AssumeRole` (for org mode)
- `ec2:Describe*`
- `organizations:List*` (for org mode)

#### Azure
- Reader role on subscriptions

#### GCP
- Compute Viewer role
- Folder Viewer role (for org mode)

### Installation

```bash
pip install git+https://github.com/yash-jhunjhunwala/multi-cloud-network-analyzer.git@v1.0.0
```

### Quick Start

```bash
# AWS single account
aws-network-analyzer --cloud aws --mode account

# AWS organization
aws-network-analyzer --cloud aws --mode org

# Azure tenant
aws-network-analyzer --cloud azure --mode tenant

# GCP organization
aws-network-analyzer --cloud gcp --mode org --key-file credentials.json
```
