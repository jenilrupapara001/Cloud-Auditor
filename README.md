<div align="center">

```
 ██████╗██╗      ██████╗ ██╗   ██╗██████╗      █████╗ ██╗   ██╗██████╗ ██╗████████╗ ██████╗ ██████╗
██╔════╝██║     ██╔═══██╗██║   ██║██╔══██╗    ██╔══██╗██║   ██║██╔══██╗██║╚══██╔══╝██╔═══██╗██╔══██╗
██║     ██║     ██║   ██║██║   ██║██║  ██║    ███████║██║   ██║██║  ██║██║   ██║   ██║   ██║██████╔╝
██║     ██║     ██║   ██║██║   ██║██║  ██║    ██╔══██║██║   ██║██║  ██║██║   ██║   ██║   ██║██╔══██╗
╚██████╗███████╗╚██████╔╝╚██████╔╝██████╔╝    ██║  ██║╚██████╔╝██████╔╝██║   ██║   ╚██████╔╝██║  ██║
 ╚═════╝╚══════╝ ╚═════╝  ╚═════╝ ╚═════╝     ╚═╝  ╚═╝ ╚═════╝ ╚═════╝ ╚═╝   ╚═╝    ╚═════╝ ╚═╝  ╚═╝
```

**Zero-Trust AWS Security & Compliance Auditing · Version 1.0 · 2026**

[![Platform](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux%20%7C%20Windows-0a0a0a?style=flat-square&logo=amazon-aws&logoColor=white)](https://github.com/jenilrupapara001/cloud-auditor/releases)
[![Engine](https://img.shields.io/badge/Engine-Go%201.22%2B-00ADD8?style=flat-square&logo=go&logoColor=white)](https://go.dev)
[![License](https://img.shields.io/badge/License-Proprietary%20EULA-FF4444?style=flat-square)](LICENSE)
[![Checks](https://img.shields.io/badge/Security%20Checks-21-22c55e?style=flat-square)](docs/CHECKS.md)
[![Frameworks](https://img.shields.io/badge/Compliance%20Frameworks-4-6366f1?style=flat-square)](docs/CHECKS.md)
[![Data](https://img.shields.io/badge/Data%20Residency-100%25%20Local-FF6B00?style=flat-square)](#privacy-model)

<br/>

> **This repository distributes pre-compiled release binaries only.**
> Cloud Auditor is proprietary software. Source code is not publicly available.
> Reverse engineering, decompilation, and redistribution are strictly prohibited.
> See [LICENSE](LICENSE) and [EULA](docs/EULA.md) for full terms.

</div>

---

## What Is Cloud Auditor?

Cloud Auditor is a **hardened, locally-executed AWS security auditing engine** built for security engineers, compliance teams, and DevSecOps practitioners who refuse to compromise on privacy or speed.

It fills the gap between free-but-limited open-source tools and prohibitively expensive enterprise platforms — delivering **military-grade security architecture, beautiful compliance reports, and sub-30-second scan times**, all without a single byte of your AWS data leaving your machine.

```
┌─────────────────────────────────────────────────────────────────┐
│                      THREAT LANDSCAPE TODAY                     │
├────────────────┬───────────────────────┬────────────────────────┤
│   Free Tools   │  Cloud Auditor        │  Enterprise (Wiz etc.) │
│   (Prowler)    │                       │                         │
├────────────────┼───────────────────────┼────────────────────────┤
│ ✅ Free        │ ✅ Affordable         │ ❌ $50k–$200k/yr       │
│ ❌ Ugly UX     │ ✅ Premium Reports    │ ✅ Polished            │
│ ✅ Local       │ ✅ 100% Local         │ ❌ Cloud-to-Cloud      │
│ ❌ Slow        │ ✅ <30s Scans         │ ✅ Fast                │
│ ❌ No Binding  │ ✅ Hardware Locked    │ ✅ SSO/SAML            │
│ ❌ Manual Map  │ ✅ Auto Compliance    │ ✅ Auto Compliance     │
└────────────────┴───────────────────────┴────────────────────────┘
```

---

## Core Principles

### 🔒 Local First — Absolute Privacy

Your AWS credentials, scan results, and security findings **never leave your machine**. All scanning is performed via read-only AWS SDK calls on your local hardware. The control plane only handles license validation — it never touches your AWS data.

### ⚡ Speed First — Parallel Execution

A highly parallelized Go engine scans all four AWS services concurrently via goroutines. Typical accounts complete in **15–30 seconds** — not minutes.

### 🛡️ Security First — Uncrackable Architecture

RSA-2048 signed responses, hardware-bound licenses, and symbol-stripped binaries form a layered defense that defeats spoofing, proxy attacks, and reverse engineering.

---

## Feature Highlights

| Feature | Details |
|---|---|
| **21 Security Checks** | S3 (5), EC2 (5), IAM (6), RDS (5) — covering all critical attack surfaces |
| **4 Compliance Frameworks** | CIS v2.0, SOC 2 Type II, HIPAA, ISO 27001:2022 — auto-mapped per finding |
| **Parallel Scan Engine** | Go goroutines — all services scanned simultaneously in one pass |
| **HTML + PDF Reports** | Glassmorphic, interactive reports with charts. PDF via headless Chrome |
| **Remediation Commands** | Copy-paste AWS CLI fix commands embedded in every finding |
| **Offline Report Gen** | Embedded HTML templates — no internet needed post-scan |
| **Hardware Binding** | SHA-256(Motherboard UUID + CPU ID) prevents key sharing |
| **RSA-2048 Integrity** | Every server response is JWS-signed; public key embedded at compile time |
| **Binary Hardening** | Symbol-stripped production builds (`-s -w`) defeat IDA Pro and Ghidra |
| **Zero Dependencies** | Single binary — no JVM, Python, Node.js, or Docker required |
| **Cross-Platform** | macOS ARM64/AMD64 · Linux AMD64 · Windows AMD64 |

---

## Quick Start

### Step 1 — Download the Binary

Grab the latest release for your platform from the [Releases](https://github.com/jenilrupapara001/cloud-auditor/releases) page, or use the commands below:

```bash
# macOS — Apple Silicon (M1/M2/M3/M4)
curl -L https://cloudauditor.io/dl/darwin-arm64 -o cloud-auditor

# macOS — Intel
curl -L https://cloudauditor.io/dl/darwin-amd64 -o cloud-auditor

# Linux — AMD64
curl -L https://cloudauditor.io/dl/linux-amd64 -o cloud-auditor

# Windows — download via browser
# https://cloudauditor.io/dl/windows-amd64.exe
```

### Step 2 — Configure AWS Credentials

Cloud Auditor uses your **existing local AWS credential chain**. No new IAM roles, cross-account trust, or console access required.

```bash
export AWS_ACCESS_KEY_ID=AKIA...
export AWS_SECRET_ACCESS_KEY=your-secret-key
export AWS_DEFAULT_REGION=us-east-1
```

> **Required IAM Policy:** `ReadOnlyAccess` (AWS managed policy).
> Cloud Auditor **never** writes, modifies, creates, or deletes any AWS resource.

**Supported credential sources** (standard AWS chain):
- Environment variables (`AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY`)
- `~/.aws/credentials` file
- AWS IAM Instance Profile (EC2)
- AWS SSO / IAM Identity Center

### Step 3 — Make Executable & Scan

```bash
chmod +x cloud-auditor

# Basic scan
./cloud-auditor scan --region us-east-1

# Multi-region scan
./cloud-auditor scan --region us-east-1,eu-west-1,ap-southeast-1

# Output formats
./cloud-auditor scan --region us-east-1 --format html   # Default — opens in browser
./cloud-auditor scan --region us-east-1 --format pdf    # Requires headless Chrome
./cloud-auditor scan --region us-east-1 --format json   # Machine-readable output
```

The scan completes in **15–30 seconds** and opens an interactive HTML report in your default browser.

### Step 4 — Activate License

Free-tier scans run immediately with no license required. To unlock Developer or Enterprise features:

```bash
./cloud-auditor login
./cloud-auditor license activate CLOUD-XXXX-XXXX-XXXX-XXXX
./cloud-auditor license status
```

See the [Pricing & Tiers](#pricing--tiers) section for feature breakdown.

---

## Security Checks Library

All **21 checks** are organized by AWS service with severity ratings, affected tiers, and remediation commands.

### S3 — Simple Storage Service

| Check ID | Name | Severity | Tier |
|---|---|---|---|
| `S3-001` | Public Access Block Missing | 🔴 CRITICAL | Free |
| `S3-002` | Incomplete Public Access Block | 🟠 HIGH | Free |
| `S3-003` | Default Encryption Disabled | 🟠 HIGH | Developer |
| `S3-004` | Server Access Logging Disabled | 🟡 MEDIUM | Developer |
| `S3-005` | Versioning Disabled | 🟢 LOW | Developer |

### EC2 — Elastic Compute Cloud

| Check ID | Name | Severity | Tier |
|---|---|---|---|
| `EC2-001` | SSH Port 22 Open to Internet (0.0.0.0/0) | 🔴 CRITICAL | Free |
| `EC2-002` | RDP Port 3389 Open to Internet | 🔴 CRITICAL | Free |
| `EC2-003` | IMDSv2 Not Enforced on Instance | 🟠 HIGH | Developer |
| `EC2-004` | EBS Volume Encryption Disabled | 🟠 HIGH | Developer |
| `EC2-005` | Instance Running Outdated AMI | 🟡 MEDIUM | Developer |

### IAM — Identity & Access Management

| Check ID | Name | Severity | Tier |
|---|---|---|---|
| `IAM-001` | Root Account MFA Disabled | 🔴 CRITICAL | Free |
| `IAM-002` | Root Account Has Active Access Keys | 🔴 CRITICAL | Free |
| `IAM-003` | IAM User Without MFA Enabled | 🟠 HIGH | Developer |
| `IAM-004` | Access Keys Not Rotated (>90 days) | 🟠 HIGH | Developer |
| `IAM-005` | User Has Inline Administrator Policy | 🟠 HIGH | Developer |
| `IAM-006` | Weak Account Password Policy | 🟡 MEDIUM | Developer |

### RDS — Relational Database Service

| Check ID | Name | Severity | Tier |
|---|---|---|---|
| `RDS-001` | Database Instance Publicly Accessible | 🔴 CRITICAL | Free |
| `RDS-002` | Storage Encryption Disabled | 🟠 HIGH | Developer |
| `RDS-003` | Automated Backups Disabled | 🟠 HIGH | Developer |
| `RDS-004` | Multi-AZ Deployment Disabled | 🟡 MEDIUM | Developer |
| `RDS-005` | Database Running on Default Port | 🟢 LOW | Developer |

> Full check specifications including AWS API calls used: [docs/CHECKS.md](docs/CHECKS.md)

---

## Compliance Framework Mapping

Every finding is automatically cross-referenced against four major compliance frameworks.

```
Finding: IAM-001 — Root Account MFA Disabled
│
├── CIS v2.0    → CIS 1.5   "Ensure MFA is enabled for the root user account"
├── SOC 2       → CC6.1     "Logical and Physical Access Controls"
├── HIPAA       → 164.312(d) "Person or Entity Authentication"
└── ISO 27001   → A.9.4.2   "Secure log-on procedures"
```

| Framework | Full Name | Tier |
|---|---|---|
| **CIS v2.0** | CIS AWS Foundations Benchmark v2.0 | Free |
| **SOC 2** | SOC 2 Type II Trust Services Criteria | Enterprise |
| **HIPAA** | HIPAA Security Rule (45 CFR Part 164) | Enterprise |
| **ISO 27001** | ISO/IEC 27001:2022 Annex A Controls | Enterprise |

Compliance mapping data is embedded in check metadata and rendered inline in all Developer and Enterprise reports.

---

## Pricing & Tiers

| Feature | Free | Developer | Enterprise |
|---|---|---|---|
| CRITICAL severity checks | ✅ 8 checks | ✅ 8 checks | ✅ 8 checks |
| HIGH / MEDIUM / LOW checks | ❌ Blurred | ✅ 13 checks | ✅ 13 checks |
| CIS v2.0 mapping | ✅ | ✅ | ✅ |
| SOC 2 / HIPAA / ISO 27001 | ❌ | ❌ | ✅ |
| HTML Reports | ✅ | ✅ | ✅ |
| PDF Export | ❌ | ✅ | ✅ |
| JSON output | ❌ | ✅ | ✅ |
| Remediation commands | ❌ | ✅ | ✅ |
| Multi-region scanning | ❌ | ✅ | ✅ |
| API access | ❌ | ❌ | ✅ |
| Priority support | ❌ | ❌ | ✅ |

---

## Security Architecture

### RSA-2048 Response Signing

Every response from the Cloud Auditor control plane is a **JWS (JSON Web Signature)** token signed with a private RSA-2048 key. The CLI validates this signature against a **public key embedded at compile time**.

This defeats three attack classes simultaneously:

```
Attack 1: DNS Spoofing
  Attacker redirects cloudauditor.io → rogue server
  Defense: RSA signature fails — rogue server has no private key ✅

Attack 2: /etc/hosts Proxy Hack
  Attacker maps cloudauditor.io → localhost proxy
  Defense: RSA signature fails — proxy cannot forge valid JWS ✅

Attack 3: mitmproxy / Charles Proxy
  Attacker intercepts HTTPS and forges response
  Defense: RSA signature fails — forged response has no valid signature ✅
```

### Hardware Identity Binding

When a license key is first activated, the control plane records a **cryptographic machine fingerprint**:

```
Fingerprint = SHA-256( Motherboard_UUID + CPU_Identifier )

Linux:   /sys/class/dmi/id/product_uuid  +  /proc/cpuinfo
macOS:   IOPlatformUUID (IOKit)          +  sysctl -n machdep.cpu.brand_string
```

On every subsequent scan, the CLI recomputes this fingerprint and includes it in the signed request. A mismatch returns **403 Forbidden**. This prevents license keys from being shared across teams or leaked to GitHub/Slack.

### Binary Hardening

Production builds are compiled with full symbol stripping:

```bash
go build -o cloud-auditor -ldflags="-s -w -X main.Version=1.0.0" ./main.go
```

| Flag | Effect |
|---|---|
| `-s` | Strips symbol table and debug information |
| `-w` | Strips DWARF debug symbol generation |
| Result | 40–60% smaller binary; IDA Pro, Ghidra, and `nm` cannot reconstruct function or variable names |

---

## Privacy Model

Cloud Auditor is built on a strict **data residency guarantee**:

```
What STAYS on your machine:
  ✅ AWS credentials (Access Key ID, Secret Key)
  ✅ All AWS API responses (S3, EC2, IAM, RDS data)
  ✅ Security findings and risk scores
  ✅ Generated HTML and PDF reports

What reaches the Cloud Auditor control plane:
  ⚠️  License key (for validation)
  ⚠️  Machine fingerprint hash (for hardware binding)
  ⚠️  Scan timestamp (for usage metering on Enterprise)

What NEVER reaches anyone:
  🔒 Your AWS Account ID, resource names, or configuration data
  🔒 IAM policies, bucket contents, or database credentials
```

---

## System Requirements

| Requirement | Minimum |
|---|---|
| **OS** | macOS 12+, Ubuntu 20.04+, Windows 10/11 |
| **Architecture** | AMD64 (x86-64) or ARM64 (Apple Silicon) |
| **AWS Permissions** | `ReadOnlyAccess` managed policy |
| **Network** | Outbound HTTPS to `cloudauditor.io` for license validation |
| **PDF Export** | Google Chrome or Chromium installed (headless mode) |
| **Disk** | ~20MB for binary; ~5MB per report |

---

## CLI Reference

```
USAGE:
  cloud-auditor <command> [flags]

COMMANDS:
  scan            Run a security audit against an AWS account
  license         Manage license activation and status
  login           Authenticate with the Cloud Auditor portal
  version         Print version and build information

SCAN FLAGS:
  --region        AWS region(s) to scan (comma-separated)    [required]
  --format        Output format: html | pdf | json           [default: html]
  --output        Output file path                           [default: ./report]
  --profile       AWS CLI profile to use
  --tier          Override tier detection (for debugging)

EXAMPLES:
  cloud-auditor scan --region us-east-1
  cloud-auditor scan --region us-east-1,eu-west-1 --format pdf
  cloud-auditor scan --region us-east-1 --profile production
  cloud-auditor license activate CLOUD-XXXX-XXXX-XXXX-XXXX
  cloud-auditor license status
```

---

## Documentation

| Document | Description |
|---|---|
| [INSTALL.md](INSTALL.md) | Platform-specific installation instructions |
| [docs/CHECKS.md](docs/CHECKS.md) | Full check specifications with AWS API references |
| [docs/FAQ.md](docs/FAQ.md) | Frequently asked questions |
| [docs/EULA.md](docs/EULA.md) | End User License Agreement |
| [CHANGELOG.md](CHANGELOG.md) | Release history and version notes |

---

## Security Vulnerability Disclosure

Cloud Auditor follows a **responsible disclosure** policy.

If you discover a security vulnerability in the binary, the control plane API, or the licensing system, please report it **privately** before any public disclosure:

- **GitHub Issues:** [Report a Vulnerability](https://github.com/jenilrupapara001/cloud-auditor/issues) *(use "Security" label)*
- **Email:** security@cloudauditor.io *(PGP key available on request)*

Please include: affected version, platform, reproduction steps, and potential impact. We target a **72-hour initial response** and **14-day patch cycle** for critical findings.

> ⚠️ **Please do not** open public issues for unpatched vulnerabilities. We appreciate coordinated disclosure.

---

## License

```
Cloud Auditor — Proprietary Software
Copyright © 2026 Cloud Auditor. All rights reserved.

The pre-compiled binaries in this repository are licensed for personal
and commercial use under the Cloud Auditor End User License Agreement.

The following are strictly prohibited without prior written consent:
  - Reverse engineering or decompilation of the binary
  - Redistribution or resale of the software
  - Modification or derivative works
  - Removal of licensing or copyright notices
  - Use to circumvent security controls or hardware binding

Full terms: https://cloudauditor.io/eula
```

---

<div align="center">

**[cloudauditor.io](https://cloudauditor.io)** · [Releases](https://github.com/USER/cloud-auditor/releases) · [Docs](docs/) · [Support](https://cloudauditor.io/support)

*Built for security engineers who don't compromise.*

</div>
