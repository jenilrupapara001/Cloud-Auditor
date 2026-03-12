<div align="center">

```
 ██████╗██╗      ██████╗ ██╗   ██╗██████╗      █████╗ ██╗   ██╗██████╗ ██╗████████╗ ██████╗ ██████╗
██╔════╝██║     ██╔═══██╗██║   ██║██╔══██╗    ██╔══██╗██║   ██║██╔══██╗██║╚══██╔══╝██╔═══██╗██╔══██╗
██║     ██║     ██║   ██║██║   ██║██║  ██║    ███████║██║   ██║██║  ██║██║   ██║   ██║   ██║██████╔╝
██║     ██║     ██║   ██║██║   ██║██║  ██║    ██╔══██║██║   ██║██║  ██║██║   ██║   ██║   ██║██╔══██╗
╚██████╗███████╗╚██████╔╝╚██████╔╝██████╔╝    ██║  ██║╚██████╔╝██████╔╝██║  ██║   ╚██████╔╝██║  ██║
 ╚═════╝╚══════╝ ╚═════╝  ╚═════╝ ╚═════╝     ╚═╝  ╚═╝ ╚═════╝ ╚═════╝ ╚═╝   ╚═╝    ╚═════╝ ╚═╝  ╚═╝
```

**Zero-Trust AWS Security & Compliance Auditing · Version 2.1.0 · 2026**

[![Platform](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux%20%7C%20Windows-0a0a0a?style=flat-square&logo=amazon-aws&logoColor=white)](https://github.com/jenilrupapara001/Cloud-Auditor/releases)
[![Engine](https://img.shields.io/badge/Engine-Go%201.26.1-00ADD8?style=flat-square&logo=go&logoColor=white)](https://go.dev)
[![License](https://img.shields.io/badge/License-Proprietary%20EULA-FF4444?style=flat-square)](LICENSE)
[![Checks](https://img.shields.io/badge/Security%20Checks-82-22c55e?style=flat-square)](#-full-security-check-library-82-checks)
[![Frameworks](https://img.shields.io/badge/Compliance%20Frameworks-4-6366f1?style=flat-square)](#-compliance-framework-mapping)
[![Data](https://img.shields.io/badge/Data%20Residency-100%25%20Local-FF6B00?style=flat-square)](#-privacy-model)

<br/>

> **This repository distributes pre-compiled release binaries and documentation.**
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
│   (Prowler)    │       (V2.1.0)        │                         │
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
A highly parallelized Go engine scans all **11 AWS services** concurrently via goroutines. Typical accounts complete in **15–30 seconds** — not minutes.

### 🛡️ Security First — Uncrackable Architecture
RSA-2048 signed responses, hardware-bound licenses, and symbol-stripped binaries form a layered defense that defeats spoofing, proxy attacks, and reverse engineering.

---

## 🔥 Master Feature List

| Feature | Details |
|---|---|
| **82 Security Checks** | S3, EC2, IAM, RDS, KMS, CloudTrail, Lambda, SNS, SQS, EKS, ECS — covering 100% of critical surfaces |
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

## 📥 Quick Start & Installation

### Step 1 — Download the Binary
Grab the latest release from the [Releases](https://github.com/jenilrupapara001/Cloud-Auditor/releases) page:

```bash
# macOS — Apple Silicon (M1/M2/M3/M4)
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.1.0/cloud-auditor-darwin-arm64 -o cloud-auditor

# Linux — AMD64
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.1.0/cloud-auditor-linux-amd64 -o cloud-auditor
```

### Step 2 — Configure AWS Credentials
Cloud Auditor uses your **existing local AWS credential chain**. No new IAM roles or cross-account trust required.

```bash
export AWS_ACCESS_KEY_ID=AKIA...
export AWS_SECRET_ACCESS_KEY=your-secret-key
export AWS_DEFAULT_REGION=us-east-1
```

> **Required IAM Policy:** `ReadOnlyAccess` (AWS managed policy).
> Cloud Auditor **never** writes, modifies, or deletes any AWS resource.

### Step 3 — Make Executable & Scan
```bash
chmod +x cloud-auditor
./cloud-auditor scan --region us-east-1
```

---

## 📚 Full Security Check Library (82 Checks)

### ☁️ S3 — Simple Storage Service (10)
| ID | Name | Severity | Tier |
|---|---|---|---|
| `S3-001` | Public Access Block Missing | 🔴 CRITICAL | Free |
| `S3-002` | Bucket ACL Public | 🔴 CRITICAL | Free |
| `S3-003` | Default Encryption Disabled | 🟠 HIGH | Developer |
| `S3-004` | Versioning Disabled | 🟡 MEDIUM | Developer |
| `S3-005` | Logging Disabled | 🟡 MEDIUM | Developer |
| `S3-006` | MFA Delete Disabled | 🟡 MEDIUM | Developer |
| `S3-007` | Lifecycle Policy Missing | 🟢 LOW | Developer |
| `S3-008` | Cross-Region Replication Off | 🟢 LOW | Developer |
| `S3-009` | Object Lock Not Enabled | 🟢 LOW | Developer |
| `S3-010` | SSL Not Enforced via Policy | 🟠 HIGH | Developer |

### 💻 EC2 — Elastic Compute Cloud (15)
| ID | Name | Severity | Tier |
|---|---|---|---|
| `EC2-001` | SSH Port 22 Open to Internet | 🔴 CRITICAL | Free |
| `EC2-002` | RDP Port 3389 Open to Internet | 🔴 CRITICAL | Free |
| `EC2.1.0` | IMDSv2 Not Enforced | 🟠 HIGH | Developer |
| `EC2-004` | EBS Volume Encryption Disabled | 🟠 HIGH | Developer |
| `EC2-005` | Stopped Instance Age > 30 Days | 🟡 MEDIUM | Developer |
| `EC2-006` | Subnet Auto-Assign Public IP | 🟠 HIGH | Developer |
| `EC2-007` | Unencrypted Snapshot Found | 🟠 HIGH | Developer |
| `EC2-008` | Default VPC In Use | 🟡 MEDIUM | Developer |
| `EC2-009` | VPC Flow Logs Disabled | 🟡 MEDIUM | Developer |
| `EC2-010` | ELB Access Logging Disabled | 🟡 MEDIUM | Developer |
| `EC2-011` | Security Group Allows All Traffic | 🟠 HIGH | Developer |
| `EC2-012` | Unused Security Group Found | 🟢 LOW | Developer |
| `EC2.1.0` | Unassociated Elastic IP | 🟢 LOW | Developer |
| `EC2-014` | MetaData Missing Mandatory Tags | 🟢 LOW | Developer |
| `EC2-015` | Instance Running Outdated AMI | 🟡 MEDIUM | Developer |

### 🔑 IAM — Identity & Access Management (15)
| ID | Name | Severity | Tier |
|---|---|---|---|
| `IAM-001` | Root Account MFA Disabled | 🔴 CRITICAL | Free |
| `IAM-002` | Root Account Has Access Keys | 🔴 CRITICAL | Free |
| `IAM-003` | User Without MFA Enabled | 🟠 HIGH | Developer |
| `IAM-004` | Access Keys Not Rotated (>90 days) | 🟠 HIGH | Developer |
| `IAM-005` | Access Keys Unused (>90 days) | 🟡 MEDIUM | Developer |
| `IAM-006` | Inline Administrator Policy Found | 🟠 HIGH | Developer |
| `IAM-007` | Managed Administrator Policy Attached | 🟠 HIGH | Developer |
| `IAM-008` | Weak Account Password Policy | 🟡 MEDIUM | Developer |
| `IAM-009` | Console Login Without MFA | 🟠 HIGH | Developer |
| `IAM-010` | Inactive User (>90 days) | 🟡 MEDIUM | Developer |
| `IAM-011` | Cross-Account Role Without ExternalID | 🟠 HIGH | Developer |
| `IAM-012` | Policy Allows Full Admin (*:*) | 🟠 HIGH | Developer |
| `IAM-013` | Empty IAM Group Found | 🟢 LOW | Developer |
| `IAM-014` | Access Analyzer Not Enabled | 🟢 LOW | Developer |
| `IAM-015` | Credential Report Stale | 🟢 LOW | Developer |

### 🗄️ RDS — Relational Database Service (10)
| ID | Name | Severity | Tier |
|---|---|---|---|
| `RDS-001` | DB Publicly Accessible | 🔴 CRITICAL | Free |
| `RDS-002` | Storage Encryption Disabled | 🟠 HIGH | Developer |
| `RDS-003` | Automated Backups Disabled | 🟠 HIGH | Developer |
| `RDS-004` | Multi-AZ Deployment Disabled | 🟡 MEDIUM | Developer |
| `RDS-005` | DB Running on Default Port | 🟢 LOW | Developer |
| `RDS-006` | Deletion Protection Disabled | 🟡 MEDIUM | Developer |
| `RDS-007` | Enhanced Monitoring Disabled | 🟡 MEDIUM | Developer |
| `RDS-008` | IAM Database Auth Disabled | 🟡 MEDIUM | Developer |
| `RDS-009` | Log Exports Not Configured | 🟡 MEDIUM | Developer |
| `RDS-010` | Unencrypted Snapshots Found | 🟠 HIGH | Developer |

### 🛠️ KMS, CloudTrail, Lambda, SNS, SQS, EKS, ECS (32)
| Service | Check ID Range | Key Focus Areas |
|---|---|---|
| **KMS** | `KMS-001` - `KMS-010` | Key rotation, policy safety, exposure, encryption context |
| **CloudTrail** | `CT-001` - `CT-005` | Multi-region logging, file validation, S3 integration, KMS |
| **Lambda** | `LMB-001` - `LMB-005` | Public access, env encryption, DLQs, VPC residency |
| **SNS/SQS** | `SNS/SQ-01–10` | Server-side encryption, policy wildcards, dead letters |
| **EKS/ECS** | `EKS/EC-01–12` | Endpoint security, logging, task definition hardening |

---

## 📈 Compliance Framework Mapping
Every finding is automatically cross-referenced against four major compliance frameworks.

```text
Finding: IAM-001 — Root Account MFA Disabled
│
├── CIS v2.0    → CIS 1.5   "Ensure MFA is enabled for the root user account"
├── SOC 2       → CC6.1     "Logical and Physical Access Controls"
├── HIPAA       → 164.312(d) "Person or Entity Authentication"
└── ISO 27001   → A.9.4.2   "Secure log-on procedures"
```

---

## 💎 Pricing & Tiers

| Feature | Free | Developer | Enterprise |
|---|---|---|---|
| CRITICAL severity checks | ✅ 8 checks | ✅ 8 checks | ✅ 8 checks |
| HIGH / MEDIUM / LOW checks | ❌ Blurred | ✅ 74 checks | ✅ 74 checks |
| CIS v2.0 mapping | ✅ | ✅ | ✅ |
| SOC 2 / HIPAA / ISO 27001 | ❌ | ❌ | ✅ |
| HTML Reports | ✅ | ✅ | ✅ |
| PDF Export | ❌ | ✅ | ✅ |
| JSON output | ❌ | ✅ | ✅ |
| Remediation commands | ❌ | ✅ | ✅ |
| Multi-region scanning | ❌ | ✅ | ✅ |
| API access | ❌ | ❌ | ✅ |

---

## 🔒 Privacy Model: Local-First
1.  **Read-Only Operations**: No AWS `write` permissions required.
2.  **No AWS Data Exfiltration**: Your account configuration never leaves your machine.
3.  **No AWS Credentials Stored**: We use your local AWS credential chain.
4.  **Local Report Rendering**: All processing happens on your local CPU.

---

<div align="center">

**[cloudauditor.io](https://cloudauditor.io)** · [Releases](https://github.com/jenilrupapara001/Cloud-Auditor/releases) · [Support](mailto:support@cloudauditor.io)

*© 2026 Cloud Auditor. All rights reserved.*

</div>
