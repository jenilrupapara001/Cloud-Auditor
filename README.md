<div align="center">


# Cloud Auditor v2.2.0


### Local-First AWS Security & Compliance Auditor — v2.2.0

**The only AWS security tool that scans, maps, and fixes — without your data ever leaving your machine.**

[![Platform](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux%20%7C%20Windows-0a0a0a?style=flat-square&logo=amazon-aws&logoColor=white)](https://github.com/jenilrupapara001/Cloud-Auditor/releases)
[![Version](https://img.shields.io/badge/Version-v2.2.0-22c55e?style=flat-square)](https://github.com/jenilrupapara001/Cloud-Auditor/releases)
[![Engine](https://img.shields.io/badge/Engine-Go%201.21+-00ADD8?style=flat-square&logo=go&logoColor=white)](https://go.dev)
[![Checks](https://img.shields.io/badge/Security%20Checks-120+-f59e0b?style=flat-square)](#8-security-checks-120-total)
[![Frameworks](https://img.shields.io/badge/Frameworks-5-6366f1?style=flat-square)](#9-compliance-frameworks)
[![Data Sent](https://img.shields.io/badge/Data%20Sent-ZERO-FF0000?style=flat-square)](#trust--security-model)
[![Stars](https://img.shields.io/github/stars/jenilrupapara001/Cloud-Auditor?style=social)](https://github.com/jenilrupapara001/Cloud-Auditor/stargazers)

<br/>

[**🚀 Get Started**](#4-quick-start-guide) · [**📋 All 120+ Checks**](#8-security-checks-120-total) · [**🔧 Auto-Fix Engine**](#6-auto-fix-engine-new-in-v220) · [**🔒 Trust Model**](#trust--security-model) · [**💰 Pricing**](#pricing) · [**📄 Changelog**](#12-changelog)

</div>

---

<div align="center">

| | 120+ | 13 | 5 | 60s | Zero |
|---|---|---|---|---|---|
| | Security Checks | AWS Services | Frameworks | First Scan | Data Sent |

</div>

---

## Why Cloud Auditor Exists

> *99% of cloud security failures are caused by misconfiguration — not by AWS being hacked. — Gartner*

Every AWS security tool available today has one of three fundamental problems:

**The "report and pray" problem** — Prowler and AWS Security Hub find issues and dump a report. The average team takes weeks to remediate. The report collects dust. Risks stay open.

**The "send us your secrets" problem** — Wiz, Vanta, and AWS Audit Manager process your resource names, account IDs, and findings on *their* infrastructure. In regulated environments (HIPAA, PCI DSS, FedRAMP), this is itself a compliance violation.

**The "costs as much as a hire" problem** — AWS Audit Manager runs ~$70k/yr at scale. Wiz starts at $100k+. These prices are inaccessible to 95% of teams that actually need the protection.

Cloud Auditor was built to solve all three at once: **local execution, auto-remediation, and a price that doesn't require a board meeting.**

---

## How We're Different — Honest Comparison

| Feature | Prowler | AWS Audit Manager | Wiz / Vanta | **Cloud Auditor v2.2.0** |
| :--- | :---: | :---: | :---: | :---: |
| **Execution** | Local (Python) | AWS Cloud (SaaS) | SaaS Cloud | ✅ **Local Go binary** |
| **Your data leaves machine?** | Prowler Cloud: Yes | ✅ Yes — AWS processes it | ✅ Yes — full access | 🔴 **NEVER** |
| **Auto-remediation** | ❌ No | ❌ No | ⚠️ Limited | ✅ **Dry-run + rollback** |
| **CI/CD native (SARIF)** | ❌ No | ❌ No | ❌ No | ✅ **GitHub Actions + SARIF** |
| **Time to first scan** | 30+ min setup | Days to weeks | Weeks | ✅ **Under 5 minutes** |
| **Packet-capture verifiable** | ❌ | ❌ | ❌ | ✅ **We have nothing to hide** |
| **Single binary** | ❌ Python deps | N/A | N/A | ✅ **curl + chmod + run** |
| **Pricing** | Free / Cloud paid | ~$70k/yr at scale | $100k–$200k/yr | ✅ **$0–$999/yr flat** |
| **Compliance frameworks** | Many | 8 | Multiple | ✅ **CIS, SOC2, HIPAA, ISO, PCI DSS** |

> **The headline:** Every other tool gives you a report. Cloud Auditor gives you a report — *and fixes it.*  
> **The headline nobody else can match:** Every other tool sends your data to their cloud. Cloud Auditor cannot — it's architecturally impossible.

---

## Trust & Security Model

> *Don't trust our marketing. Verify it yourself.*

This is the section most tools skip. We don't.

### What actually leaves your machine during a scan

| Data | Leaves your machine? |
| :--- | :---: |
| HTTPS calls to `*.amazonaws.com` (read-only SDK) | ✅ Yes — AWS needs this |
| SHA-256 machine fingerprint + score (license check) | ✅ Yes — one call, score number only |
| **AWS credentials** | 🔴 **NEVER** |
| **Resource names (bucket names, instance IDs)** | 🔴 **NEVER** |
| **Scan findings** | 🔴 **NEVER** |
| **Account IDs** | 🔴 **NEVER** |

### Four ways to verify this yourself

**1. Run a packet capture during scan**
```bash
# macOS
sudo tcpdump -i any -w capture.pcap &
cloud-auditor scan
kill %1
tcpdump -r capture.pcap | grep -v amazonaws.com
```
You will see only: HTTPS to `*.amazonaws.com` + one call to the license server. No resource data. No findings. No account names. Anywhere.

**2. Inspect the read-only IAM policy**
Cloud Auditor only needs `Describe*`, `List*`, and `Get*` permissions. No write actions. You can paste the required policy to your security team in 30 seconds — there's nothing to hide.

**3. Dry-run default on every fix**
Nothing changes in your AWS account unless you explicitly pass `--no-dry-run` and confirm. Every fix is logged with the original resource state for complete rollback.

**4. Open source scan logic on GitHub**
Read the scan engine. Verify every API call. Confirm there's no telemetry beyond what's listed above. [github.com/jenilrupapara001/Cloud-Auditor](https://github.com/jenilrupapara001/Cloud-Auditor) — nothing hidden.

### Who specifically should trust Cloud Auditor

- **Regulated environments** (HIPAA, PCI DSS, FedRAMP) where sending resource data to a SaaS vendor is itself a compliance violation
- **Air-gapped or restricted networks** where cloud SaaS tools simply cannot be installed
- **Freelancers auditing client accounts** who cannot hand client AWS data to a third party
- **Startups pre-SOC 2** who need compliance evidence without a $70k/yr tool

---

## 1. Introduction & What's New in v2.2.0

Cloud Auditor is a hardened, locally-executed AWS security auditing engine designed for security-first engineering teams. It provides comprehensive coverage across 13 AWS services with 120+ built-in checks — all running exclusively on your own hardware.

**Version 2.2.0 is the Fix Release.** It ships three capabilities that AWS Audit Manager fundamentally cannot offer: an auto-fix engine with rollback, native CI/CD integration with SARIF output, and 38 new security checks covering WAF, Secrets Manager, ACM, ElastiCache, OpenSearch, and AWS Config.

### 1.1 Core Philosophy

- **Local First** — AWS credentials and scan data never leave your machine. All scanning runs via read-only SDK calls locally.
- **Fix First** — Every finding ships with an exact `aws-cli` command. v2.2.0 adds one-command auto-fix with dry-run and rollback.
- **CI/CD Native** — SARIF output, GitHub Actions, score-delta gates — security becomes part of every pull request.
- **Compliance Ready** — Automated mapping to CIS v2.0, SOC 2, HIPAA, ISO 27001, and new in v2.2.0: PCI DSS v4.0.
- **Speed First** — Highly parallelized Go engine. 120+ checks across 13 services complete in under 60 seconds.

### 1.2 v2.2.0 Changelog Summary

| Area | Change | Impact |
| :--- | :--- | :--- |
| **Auto-Fix Engine** | `cloud-auditor fix` with dry-run + rollback | **NEW** |
| **CI/CD Integration** | SARIF output + GitHub Actions Marketplace action | **NEW** |
| **Security Checks** | 38 new checks (WAF, Secrets Mgr, ACM, ElastiCache, OpenSearch, Config) | **NEW** |
| **Frameworks** | PCI DSS v4.0 added — 5 frameworks total | **NEW** |
| **Dashboard** | Inline fix commands, score trend, checklist mode, executive PDF | **ENHANCED** |
| **Multi-region** | `cloud-auditor scan --all-regions` parallel scan | **NEW** |
| **Alerts** | Slack and Microsoft Teams webhook notifications | **NEW** |
| **Install script** | `curl -sSL https://cloudauditor.vercel.app/install.sh \| bash` now live | **LIVE** |

---

## 2. System Requirements

### 2.1 Hardware

| Component | Minimum | Recommended |
| :--- | :--- | :--- |
| **CPU** | 2 cores | 4+ cores |
| **RAM** | 4 GB | 8+ GB |
| **Disk** | 500 MB | 1 GB |
| **Network** | Internet connection | Broadband |

### 2.2 Software

| Requirement | Version / Notes |
| :--- | :--- |
| **Operating System** | macOS 10.15+, Ubuntu 18.04+, CentOS 7+, Windows 10+ |
| **Go** | 1.21+ (only if building from source) |
| **Node.js** | 18+ (only if running dashboard locally) |
| **AWS CLI** | Latest (optional, for manual remediation commands) |
| **Docker** | Only required for LocalStack sandbox testing |

### 2.3 AWS Requirements

- AWS Account with IAM user/role
- AWS Access Key ID and Secret Access Key
- `ReadOnlyAccess` policy OR custom least-privilege policy (see [Section 14](#14-architecture--security-model))
- **For auto-fix**: IAM user additionally needs write permissions on the services being fixed

---

## 3. Installation

### 3.1 One-Line Install (Recommended)

```bash
curl -sSL https://cloudauditor.vercel.app/install.sh | bash
```

Auto-detects your OS and architecture, downloads the correct binary, makes it executable, and optionally adds it to PATH.

### 3.2 Manual Binary Download

**macOS Apple Silicon (M1/M2/M3/M4)**
```bash
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.2.0/cloud-auditor-darwin-arm64 -o ~/cloud-auditor
chmod +x ~/cloud-auditor
```

**macOS Intel (x86_64)**
```bash
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.2.0/cloud-auditor-darwin-amd64 -o ~/cloud-auditor
chmod +x ~/cloud-auditor
```

**Linux AMD64**
```bash
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.2.0/cloud-auditor-linux-amd64 -o ~/cloud-auditor
chmod +x ~/cloud-auditor
```

**Linux ARM64 (Graviton)**
```bash
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.2.0/cloud-auditor-linux-arm64 -o ~/cloud-auditor
chmod +x ~/cloud-auditor
```

**Windows (PowerShell)**
```powershell
Invoke-WebRequest -Uri https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.2.0/cloud-auditor-windows-amd64.exe -OutFile cloud-auditor.exe
```

### 3.3 System-Wide Install

```bash
sudo mv ~/cloud-auditor /usr/local/bin/cloud-auditor
cloud-auditor version
```

### 3.4 macOS Security Warning Fix

```bash
xattr -d com.apple.quarantine ~/cloud-auditor
```

Or: **System Settings → Privacy & Security → Allow Anyway**

### 3.5 Build from Source

```bash
git clone https://github.com/jenilrupapara001/Cloud-Auditor-CLI.git
cd Cloud-Auditor-CLI
go build -o cloud-auditor -ldflags="-s -w" main.go
```

### 3.6 Verify Installation

```bash
cloud-auditor version
# Expected: cloud-auditor v2.2.0
```

---

## 4. Quick Start Guide

From zero to your first security report in under 5 minutes.

**Step 1 — Install**
```bash
curl -sSL https://cloudauditor.vercel.app/install.sh | bash
```

**Step 2 — Configure AWS Credentials**

Option A: Environment variables (recommended)
```bash
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
export AWS_DEFAULT_REGION=us-east-1
```

Option B: Interactive wizard
```bash
cloud-auditor configure
```

Option C: Named AWS profile
```bash
cloud-auditor scan --profile my-aws-profile --region us-east-1
```

**Step 3 — Run your first scan**
```bash
cloud-auditor scan
```

The dashboard opens automatically at `http://localhost:3001/findings-dashboard` with your full report.

**Step 4 — Fix critical findings**
```bash
# Preview all changes before anything runs
cloud-auditor fix --dry-run --severity critical

# Apply fixes — rollback log saved to ~/.cloud-auditor/rollback.json
cloud-auditor fix --severity critical
```

---

## 5. CLI Commands Reference

### 5.1 Main Commands

| Command | Description |
| :--- | :--- |
| `cloud-auditor scan` | Run a full security scan |
| `cloud-auditor fix` | Auto-fix findings *(NEW in v2.2.0)* |
| `cloud-auditor configure` | Interactive setup wizard |
| `cloud-auditor login` | Authenticate with license key |
| `cloud-auditor logout` | Remove stored license |
| `cloud-auditor status` | Show license tier and expiry |
| `cloud-auditor version` | Display version number |
| `cloud-auditor update` | Update to latest version |
| `cloud-auditor checks --list` | List all 120+ checks with details |

### 5.2 Scan Flags

| Flag | Short | Default | Description |
| :--- | :--- | :--- | :--- |
| `--region` | `-r` | `us-east-1` | AWS region to scan |
| `--all-regions` | — | `false` | Scan all AWS regions in parallel *(NEW)* |
| `--profile` | `-p` | `default` | AWS CLI profile to use |
| `--output` | `-o` | `html` | Format: `html`, `json`, `pdf`, `sarif` *(NEW)* |
| `--framework` | `-f` | `all` | Filter: `soc2`, `hipaa`, `cis`, `iso27001`, `pcidss` *(NEW)* |
| `--services` | `-s` | `all` | Filter: `s3`, `ec2`, `iam`, `rds`, `waf`, `secretsmanager`, ... |
| `--severity` | — | `all` | Filter: `critical`, `high`, `medium`, `low` |
| `--open` | — | `true` | Auto-open dashboard after scan |
| `--port` | — | `3001` | Dashboard server port |
| `--fail-if-score-drops-by` | — | — | Exit code 1 if score drops by N points *(NEW)* |

### 5.3 Fix Flags *(NEW in v2.2.0)*

| Flag | Default | Description |
| :--- | :--- | :--- |
| `--severity` | `critical` | Fix findings at this level: `critical`, `high`, `medium`, `all` |
| `--id` | — | Fix a single finding by check ID, e.g. `--id EC2-001` |
| `--dry-run` | `false` | Show exactly what would change — nothing is applied |
| `--services` | `all` | Limit fixes to specific services: `--services s3,iam` |
| `--rollback` | — | Undo the last fix session using the rollback log |

### 5.4 Usage Examples

**Basic scans**
```bash
cloud-auditor scan                                   # Full scan, HTML report
cloud-auditor scan -r us-west-2 -o pdf              # PDF output, specific region
cloud-auditor scan --all-regions -o json            # All regions, JSON output
cloud-auditor scan --services s3,iam                # Specific services only
```

**Compliance scans**
```bash
cloud-auditor scan --framework soc2 -o pdf          # SOC 2 PDF report
cloud-auditor scan --framework hipaa                # HIPAA check
cloud-auditor scan --framework pcidss               # PCI DSS v4.0 (NEW)
cloud-auditor scan --framework cis                  # CIS v2.0 benchmark
```

**Auto-fix**
```bash
cloud-auditor fix --dry-run --severity critical     # Preview critical fixes
cloud-auditor fix --severity critical               # Apply critical fixes
cloud-auditor fix --id S3-001                       # Fix one specific check
cloud-auditor fix --severity high --services s3,ec2 # Fix high findings in S3+EC2
cloud-auditor fix --rollback                        # Undo last fix session
```

**CI/CD pipeline**
```bash
cloud-auditor scan --output sarif > results.sarif   # GitHub Security tab native
cloud-auditor scan --output json > findings.json    # Machine-readable for pipelines
cloud-auditor scan --fail-if-score-drops-by 10     # Fail build if score drops
```

---

## 6. Auto-Fix Engine *(NEW in v2.2.0)*

> *Every other tool gives you a report. Cloud Auditor gives you a report — and fixes it.*
> *This is the feature AWS Audit Manager can never have, because it runs on their cloud, not yours.*

### 6.1 How It Works

1. `cloud-auditor fix` reads the most recent scan from `web/scans/latest.json`
2. For each qualifying finding, it maps the check ID to its fix logic
3. In **dry-run mode**, every proposed action is printed — nothing is changed
4. In **apply mode**, each fix runs via the AWS SDK with explicit confirmation
5. Every change is logged to `~/.cloud-auditor/rollback.json` with the original resource state
6. `cloud-auditor fix --rollback` reverses all changes in reverse order

### 6.2 Fix Coverage by Service

| Service | Fixable Checks | Example Auto-Fix |
| :--- | :--- | :--- |
| **S3** | S3-001 to S3-005 | Block public access, enable encryption, enable versioning |
| **EC2** | EC2-001 to EC2-009 | Revoke open SSH/RDP, enforce IMDSv2, enable EBS encryption |
| **IAM** | IAM-002 to IAM-008 | Delete root access keys, rotate old keys, fix password policy |
| **RDS** | RDS-001 to RDS-006 | Disable public access, enable backups, enable Multi-AZ |
| **KMS** | KMS-001 to KMS-003 | Enable key rotation |
| **CloudTrail** | CT-001 to CT-003 | Enable trail, enable file validation, enable multi-region |
| **Secrets Mgr** | SM-001, SM-002 | Enable rotation, delete unused secrets *(NEW)* |

### 6.3 Dry-Run Output Example

```bash
$ cloud-auditor fix --dry-run --severity critical

DRY RUN MODE — No changes will be applied
Found 3 critical findings to fix:

[1/3] S3-001: Public Access Block Missing on bucket: my-prod-bucket
      Would run: aws s3api put-public-access-block --bucket my-prod-bucket \
        --public-access-block-configuration '{"BlockPublicAcls":true,...}'

[2/3] EC2-001: SSH Port 22 Open to Internet on sg-0abc1234
      Would run: aws ec2 revoke-security-group-ingress --group-id sg-0abc1234 \
        --protocol tcp --port 22 --cidr 0.0.0.0/0

[3/3] IAM-002: Root Account Has Access Keys
      Would run: aws iam delete-access-key --access-key-id AKIA...

Run without --dry-run to apply all 3 fixes.
```

---

## 7. CI/CD & DevOps Integration *(NEW in v2.2.0)*

Cloud Auditor v2.2.0 is the first local AWS security tool with native CI/CD integration. Run it in any pipeline, block deploys on regressions, and post findings directly to GitHub's Security tab.

### 7.1 GitHub Actions — Basic Setup

```yaml
# .github/workflows/cloud-auditor.yml
name: Cloud Auditor Security Scan
on: [push, pull_request]

jobs:
  security-scan:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
      contents: read
    steps:
      - uses: actions/checkout@v4

      - name: Install Cloud Auditor
        run: curl -sSL https://cloudauditor.vercel.app/install.sh | bash

      - name: Run Security Scan
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: us-east-1
        run: cloud-auditor scan --output sarif > results.sarif

      - name: Upload to GitHub Security Tab
        uses: github/codeql-action/upload-sarif@v3
        with:
          sarif_file: results.sarif
```

### 7.2 Advanced — Block PRs on Score Regression

```yaml
      - name: Score-Delta Gate
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: cloud-auditor scan --fail-if-score-drops-by 5 --output json
        # Exits with code 1 if security score drops by 5+ points vs last scan
```

---

## 8. Security Checks (120+ Total)

### 8.1 S3 — Simple Storage Service (10 checks)

| ID | Name | Severity | Tier |
| :--- | :--- | :--- | :--- |
| `S3-001` | Public Access Block Missing | 🔴 CRITICAL | Free |
| `S3-002` | Bucket ACL Public | 🔴 CRITICAL | Free |
| `S3-003` | Default Encryption Disabled | 🟠 HIGH | Enterprise |
| `S3-004` | Versioning Disabled | 🟡 MEDIUM | Enterprise |
| `S3-005` | Logging Disabled | 🟡 MEDIUM | Enterprise |
| `S3-006` | MFA Delete Disabled | 🟡 MEDIUM | Enterprise |
| `S3-007` | Lifecycle Policy Missing | 🟢 LOW | Enterprise |
| `S3-008` | Cross-Region Replication Off | 🟢 LOW | Enterprise |
| `S3-009` | Object Lock Not Enabled | 🟢 LOW | Enterprise |
| `S3-010` | SSL Not Enforced via Policy | 🟠 HIGH | Enterprise |

### 8.2 EC2 — Elastic Compute Cloud (15 checks)

| ID | Name | Severity | Tier |
| :--- | :--- | :--- | :--- |
| `EC2-001` | SSH Port 22 Open to Internet | 🔴 CRITICAL | Free |
| `EC2-002` | RDP Port 3389 Open to Internet | 🔴 CRITICAL | Free |
| `EC2-003` | IMDSv2 Not Enforced | 🟠 HIGH | Enterprise |
| `EC2-004` | EBS Volume Encryption Disabled | 🟠 HIGH | Enterprise |
| `EC2-005` | Stopped Instance Age > 30 Days | 🟡 MEDIUM | Enterprise |
| `EC2-006` | Subnet Auto-Assign Public IP | 🟠 HIGH | Enterprise |
| `EC2-007` | Unencrypted Snapshot Found | 🟠 HIGH | Enterprise |
| `EC2-008` | Default VPC In Use | 🟡 MEDIUM | Enterprise |
| `EC2-009` | VPC Flow Logs Disabled | 🟡 MEDIUM | Enterprise |
| `EC2-010` | ELB Access Logging Disabled | 🟡 MEDIUM | Enterprise |
| `EC2-011` | Security Group Allows All Traffic | 🟠 HIGH | Enterprise |
| `EC2-012` | Unused Security Group Found | 🟢 LOW | Enterprise |
| `EC2-013` | Unassociated Elastic IP | 🟢 LOW | Enterprise |
| `EC2-014` | Missing Mandatory Tags | 🟢 LOW | Enterprise |
| `EC2-015` | Instance Running Outdated AMI | 🟡 MEDIUM | Enterprise |

### 8.3 IAM — Identity & Access Management (15 checks)

| ID | Name | Severity | Tier |
| :--- | :--- | :--- | :--- |
| `IAM-001` | Root Account MFA Disabled | 🔴 CRITICAL | Free |
| `IAM-002` | Root Account Has Access Keys | 🔴 CRITICAL | Free |
| `IAM-003` | User Without MFA Enabled | 🟠 HIGH | Enterprise |
| `IAM-004` | Access Keys Not Rotated (>90 days) | 🟠 HIGH | Enterprise |
| `IAM-005` | Access Keys Unused (>90 days) | 🟡 MEDIUM | Enterprise |
| `IAM-006` | Inline Administrator Policy Found | 🟠 HIGH | Enterprise |
| `IAM-007` | Managed Administrator Policy Attached | 🟠 HIGH | Enterprise |
| `IAM-008` | Weak Account Password Policy | 🟡 MEDIUM | Enterprise |
| `IAM-009` | Console Login Without MFA | 🟠 HIGH | Enterprise |
| `IAM-010` | Inactive User (>90 days) | 🟡 MEDIUM | Enterprise |
| `IAM-011` | Cross-Account Role Without ExternalID | 🟠 HIGH | Enterprise |
| `IAM-012` | Policy Allows Full Admin (*:*) | 🟠 HIGH | Enterprise |
| `IAM-013` | Empty IAM Group Found | 🟢 LOW | Enterprise |
| `IAM-014` | Access Analyzer Not Enabled | 🟢 LOW | Enterprise |
| `IAM-015` | Credential Report Stale | 🟢 LOW | Enterprise |

### 8.4 RDS — Relational Database Service (10 checks)

| ID | Name | Severity | Tier |
| :--- | :--- | :--- | :--- |
| `RDS-001` | DB Publicly Accessible | 🔴 CRITICAL | Free |
| `RDS-002` | Storage Encryption Disabled | 🟠 HIGH | Enterprise |
| `RDS-003` | Automated Backups Disabled | 🟠 HIGH | Enterprise |
| `RDS-004` | Multi-AZ Deployment Disabled | 🟡 MEDIUM | Enterprise |
| `RDS-005` | DB Running on Default Port | 🟢 LOW | Enterprise |
| `RDS-006` | Deletion Protection Disabled | 🟡 MEDIUM | Enterprise |
| `RDS-007` | Enhanced Monitoring Disabled | 🟡 MEDIUM | Enterprise |
| `RDS-008` | IAM Database Auth Disabled | 🟡 MEDIUM | Enterprise |
| `RDS-009` | Log Exports Not Configured | 🟡 MEDIUM | Enterprise |
| `RDS-010` | Unencrypted Snapshots Found | 🟠 HIGH | Enterprise |

### 8.5 New Services in v2.2.0

| Service | Checks | Key Findings |
| :--- | :--- | :--- |
| **WAF** | 8 | Rules enabled, logging on, rate limiting configured, SQLi/XSS rules |
| **Secrets Manager** | 6 | Rotation enabled, unused secrets, plaintext secrets in env vars |
| **ACM** | 7 | Expiring certs (<30 days), expired certs, wildcard cert usage |
| **ElastiCache** | 6 | Encryption in-transit/at-rest, Redis AUTH disabled |
| **OpenSearch** | 6 | VPC placement, public access policies, node-to-node encryption |
| **AWS Config** | 5 | Recorder not enabled, delivery channel missing, rules not deployed |

### 8.6 Existing Services

| Service | Checks | Key Focus Areas |
| :--- | :--- | :--- |
| **KMS** | 10 | Key rotation, policy safety, encryption context |
| **CloudTrail** | 5 | Multi-region logging, file validation, S3 integration |
| **Lambda** | 5 | Public access, env encryption, DLQs, VPC residency |
| **SNS/SQS** | 10 | Server-side encryption, policy wildcards, dead letters |
| **EKS/ECS** | 12 | Endpoint security, logging, task definition hardening |

---

## 9. Compliance Frameworks

Every finding is automatically cross-referenced against every applicable framework at scan time — no extra configuration required.

```
Finding: IAM-001 — Root Account MFA Disabled
│
├── CIS v2.0    → CIS 1.5    "Ensure MFA is enabled for the root user account"
├── SOC 2       → CC6.1      "Logical and Physical Access Controls"
├── HIPAA       → §164.312(d) "Person or Entity Authentication"
├── ISO 27001   → A.9.4.2    "Secure log-on procedures"
└── PCI DSS     → Req 8.4    "MFA for all access into CDE" (NEW)
```

| Framework | Checks | Tier | Notes |
| :--- | :--- | :--- | :--- |
| **CIS AWS Foundations v2.0** | 45+ | **Free** | All teams — baseline AWS hardening |
| **SOC 2 Type II** | 55+ | **Enterprise** | SaaS companies preparing for audits |
| **HIPAA Security Rule** | 45+ | **Enterprise** | Healthcare and health-tech |
| **ISO 27001:2022** | 55+ | **Enterprise** | Enterprise and global operations |
| **PCI DSS v4.0** | 40+ | **Enterprise** | Any team handling card payments *(NEW)* |

---

## 10. Dashboard Guide

URL: `http://localhost:3001/findings-dashboard` — opens automatically after every scan.

| Feature | Description |
| :--- | :--- |
| **Findings table** | Searchable, sortable, paginated — inline fix commands visible without clicking |
| **Score trend line** | Security score across last 10 scans |
| **Fix-it checklist** | Mark findings in-progress or resolved — state persists between sessions |
| **Executive summary** | Score, delta, top 3 risks — 30-second management briefing |
| **Scan comparison** | Side-by-side diff between any two scans: new, resolved, unchanged |
| **One-click PDF** | Branded compliance report — no re-scan needed |

---

## 11. Alerts & Multi-Region *(NEW in v2.2.0)*

### Slack & Teams Notifications

```json
{
  "slack_webhook": "https://hooks.slack.com/services/...",
  "alert_on_severity": ["critical", "high"],
  "alert_mode": "new_only"
}
```

Alert modes: `new_only` (no alert fatigue), `all`, or `daily_digest`. Payload includes score, delta, new finding count by severity, and check names — never resource IDs.

### Multi-Region Scanning

```bash
cloud-auditor scan --all-regions
```

Scans all 20+ AWS regions simultaneously using Go goroutines. Global services (IAM, KMS, CloudTrail) run once. Dashboard shows aggregate score plus per-region breakdown. Performance: 60–120 seconds for a small account across all regions.

---

## 12. LocalStack Sandbox Testing

Test the full scan and auto-fix engine without a real AWS account:

```bash
export AWS_ENDPOINT_URL=http://localhost:4566
cloud-auditor scan --region us-east-1
```

---

## 13. Architecture & Security Model

```
Your Machine
│
├── 1. Credentials  ──── reads from env vars / config (never written to disk)
│
├── 2. Parallel Scan ─── Go goroutines hit AWS read-only APIs for all 13 services
│
├── 3. Check Engine ──── 120+ functions evaluate responses in local RAM
│
├── 4. Results ──────── saved to local web/scans/ — no upload, no cloud sync
│
└── 5. Dashboard ────── Next.js reads local JSON — no backend, no server

What leaves your machine:
  ✅ HTTPS to *.amazonaws.com   (AWS needs this to respond)
  ✅ Machine hash + score        (license validation only)

What NEVER leaves your machine:
  🔴 AWS credentials
  🔴 Resource names
  🔴 Scan findings
  🔴 Account IDs
```

**Required IAM permissions:** `Describe*`, `List*`, `Get*` only. Cloud Auditor never calls write APIs during scan. Fix commands only execute when explicitly invoked via `cloud-auditor fix`.

---

## 14. Troubleshooting & FAQ

**Q: Will Cloud Auditor modify my AWS resources without asking?**
No. Scans are 100% read-only. The fix engine only runs when you explicitly invoke `cloud-auditor fix`, and dry-run is the default every time.

**Q: Can I verify that no data leaves my machine?**
Yes — run a packet capture during a scan (see [Trust & Security Model](#trust--security-model)). You'll see only HTTPS to `*.amazonaws.com` and one license validation call. Everything else stays local.

**Q: Can I use it in CI/CD pipelines?**
Yes. Use `--output sarif` for GitHub Security tab integration, or `--output json` for custom pipelines. A `--fail-if-score-drops-by N` flag lets you block PRs that introduce regressions.

**Q: What happens after my 1-week Enterprise trial?**
Your account reverts to the Free tier automatically. All scan history is preserved. Upgrade anytime at [cloudauditor.vercel.app](https://cloudauditor.vercel.app).

**Q: Do I need Docker or Python installed?**
No. Cloud Auditor is a single Go binary with zero runtime dependencies. One `curl` command and you're scanning.

**Q: I'm a freelancer auditing a client's AWS account. Is this safe?**
Yes — this is one of our primary use cases. Your client's resource names and findings never leave their machine (or yours). You can show them the packet capture proof in the same meeting.

**Q: Is the source code available?**
The scan logic and check engine are available on GitHub. The binary release is proprietary. You can read every API call we make, verify there's no telemetry beyond the license check, and confirm the privacy model before trusting us with a single command.

---

## Pricing

No per-resource billing. No scaling surprises. Flat annual pricing.

| Feature | Free | Enterprise |
| :--- | :---: | :---: |
| CRITICAL severity checks | ✅ 8 checks | ✅ All 120+ checks |
| CIS v2.0 framework | ✅ | ✅ |
| SOC 2 / HIPAA / ISO 27001 / PCI DSS | ❌ | ✅ |
| HTML reports | ✅ | ✅ |
| PDF export | ❌ | ✅ |
| JSON + SARIF output | ❌ | ✅ |
| Remediation commands | ❌ | ✅ |
| Auto-fix engine | ❌ | ✅ |
| Multi-region scanning | ❌ | ✅ |
| GitHub Actions + SARIF | ❌ | ✅ |
| Slack / Teams alerts | ❌ | ✅ |
| **Price** | **$0/year** | **$999/year** |

> 1-week Enterprise free trial at [cloudauditor.vercel.app](https://cloudauditor.vercel.app) — no credit card required.

| Tool | Annual Cost |
| :--- | :--- |
| **Cloud Auditor Enterprise** | **$999/yr** |
| Prowler Cloud | ~$2k–5k/yr |
| AWS Audit Manager | ~$70k/yr* |
| Wiz | ~$100k+/yr |

*Medium account, 100 accounts, monthly pricing

---

## Roadmap

| Version | Target | Features |
| :--- | :--- | :--- |
| **v2.2.0** | **NOW** | Auto-fix engine, GitHub Actions, SARIF, PCI DSS v4.0, multi-region, alerts |
| **v2.3** | Q2 2026 | IaC drift detection (Terraform/CDK), NIST 800-53, multi-account single scan, continuous monitoring |
| **v3.0** | H2 2026 | Custom check YAML DSL, community checks registry, policy-as-code engine, SSO/SAML, multi-account org dashboards |

---

<div align="center">

**[Dashboard & Docs](https://cloudauditor.vercel.app)** · **[GitHub Repo](https://github.com/jenilrupapara001/Cloud-Auditor)** · **[Releases](https://github.com/jenilrupapara001/Cloud-Auditor/releases)** · **[Start Free Trial](https://cloudauditor.vercel.app/signup)**

<br/>

*Your AWS credentials, resource names, and scan results NEVER leave your machine.*

© 2026 Cloud Auditor. Built for the privacy-conscious cloud.

</div>
