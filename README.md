# CLOUD AUDITOR  v2.2.0
Local-First AWS Security & Compliance Auditor
Complete README Enterprise Edition

120+
Security Checks
13
AWS Services
5
Frameworks
60s
First Scan
Zero
Data Sent

---

## 1. Introduction & What's New in v2.2.0
Cloud Auditor is a hardened, locally-executed AWS security auditing engine designed for security-first engineering teams. It provides comprehensive coverage across 13 AWS services with 120+ built-in checks all running exclusively on your own hardware.
Version 2.2.0 is the Fix Release. It ships three capabilities that AWS Audit Manager fundamentally cannot offer: an auto-fix engine, native CI/CD integration with SARIF output, and 38 new security checks covering WAF, Secrets Manager, ACM, ElastiCache, OpenSearch, and AWS Config.

### 1.1 Core Philosophy
- **Local First**:  AWS credentials and scan data never leave your machine. All scanning runs via read-only SDK calls locally.
- **Fix First**:  Every finding ships with an exact aws-cli command. v2.2.0 adds one-command auto-fix with dry-run and rollback.
- **CI/CD Native**:  SARIF output, GitHub Actions, score-delta gates—security becomes part of every pull request.
- **Compliance Ready**:  Automated mapping to CIS v2.0, SOC 2, HIPAA, ISO 27001, and new in v2.2.0: PCI DSS v4.0.
- **Speed First**:  Highly parallelized Go engine. 120+ checks across 13 services complete in under 60 seconds.

### 1.2 v2.2.0 Changelog Summary
| Area | Change | Impact |
| :--- | :--- | :--- |
| **Auto-Fix Engine** | `cloud-auditor fix` command with dry-run + rollback | **NEW** |
| **CI/CD Integration** | SARIF output + GitHub Actions Marketplace action | **NEW** |
| **Security Checks** | 38 new checks (WAF, Secrets Mgr, ACM, ElastiCache, OpenSearch, Config) | **NEW** |
| **Frameworks** | PCI DSS v4.0 added—5 frameworks total | **NEW** |
| **Dashboard** | Inline fix commands, score trend, checklist mode, executive PDF | **ENHANCED** |
| **Multi-region** | `cloud-auditor scan --all-regions` parallel scan | **NEW** |
| **Alerts** | Slack and Microsoft Teams webhook notifications | **NEW** |
| **Install script** | `curl -sSL https://cloudauditor.vercel.app/install.sh | bash` now live | **LIVE** |

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
- `ReadOnlyAccess` policy OR custom least-privilege policy (see Section 12)
- **For auto-fix**: IAM user additionally needs write permissions on the services being fixed

---

## 3. Installation
### 3.1 One-Line Install (Recommended — New in v2.2.0)
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
Or: **System Settings > Privacy & Security > Allow Anyway**

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

**Step 1: Install the binary**
```bash
curl -sSL https://cloudauditor.io/install.sh | bash
```

**Step 2: Configure AWS Credentials**
- **Option A: Environment Variables (Recommended)**
  ```bash
  export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
  export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
  export AWS_DEFAULT_REGION=us-east-1
  ```
- **Option B: Interactive Wizard**
  ```bash
  cloud-auditor configure
  ```
- **Option C: Named AWS Profile**
  ```bash
  cloud-auditor scan --profile my-aws-profile --region us-east-1
  ```

**Step 3: Run Your First Scan**
```bash
cloud-auditor scan
```
The dashboard opens automatically at `http://localhost:3001/findings-dashboard` with your full report.

**Step 4: Fix Critical Findings (New in v2.2.0)**
```bash
cloud-auditor fix --dry-run --severity critical
# Preview all changes without applying them

cloud-auditor fix --severity critical
# Apply fixes. Rollback log saved to ~/.cloud-auditor/rollback.json
```

---

## 5. CLI Commands Reference
### 5.1 Main Commands
| Command | Description |
| :--- | :--- |
| `cloud-auditor scan` | Run a full security scan |
| `cloud-auditor fix` | Auto-fix findings (NEW in v2.2.0) |
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
| `--all-regions` | — | `false` | Scan all AWS regions in parallel (NEW v2.2.0) |
| `--profile` | `-p` | `default` | AWS CLI profile to use |
| `--output` | `-o` | `html` | Format: `html`, `json`, `pdf`, `sarif` (NEW v2.2.0) |
| `--framework` | `-f` | `all` | Filter: `soc2`, `hipaa`, `cis`, `iso27001`, `pcidss` (NEW) |
| `--services` | `-s` | `all` | Filter: `s3`, `ec2`, `iam`, `rds`, `waf`, `secretsmanager`, ... |
| `--severity` | — | `all` | Filter: `critical`, `high`, `medium`, `low` |
| `--open` | — | `true` | Auto-open dashboard after scan |
| `--port` | — | `3001` | Dashboard server port |
| `--fail-if-score-drops-by` | — | — | Exit code 1 if score drops by N points (NEW) |

### 5.3 Fix Flags (NEW in v2.2.0)
| Flag | Default | Description |
| :--- | :--- | :--- |
| `--severity` | `critical` | Fix findings at this severity level: `critical`, `high`, `medium`, `all` |
| `--id` | — | Fix a single finding by its check ID, e.g. `--id EC2-001` |
| `--dry-run` | `false` | Show exactly what would change without applying anything |
| `--services` | `all` | Limit fixes to specific services: `--services s3,iam` |
| `--rollback` | — | Undo the last fix session using the rollback log |

### 5.4 Usage Examples
**Basic scans**
```bash
cloud-auditor scan                                    # Full scan, HTML report
cloud-auditor scan -r us-west-2 -o pdf               # PDF output, specific region
cloud-auditor scan --all-regions -o json             # All regions, JSON output
cloud-auditor scan --services s3,iam                 # Specific services only
```

**Compliance scans**
```bash
cloud-auditor scan --framework soc2 -o pdf           # SOC 2 PDF report
cloud-auditor scan --framework hipaa                 # HIPAA check
cloud-auditor scan --framework pcidss                # PCI DSS v4.0 (NEW)
cloud-auditor scan --framework cis                   # CIS v2.0 benchmark
```

**Auto-fix (NEW in v2.2.0)**
```bash
cloud-auditor fix --dry-run --severity critical      # Preview critical fixes
cloud-auditor fix --severity critical                # Apply critical fixes
cloud-auditor fix --id S3-001                       # Fix one specific check
cloud-auditor fix --severity high --services s3,ec2 # Fix high findings in S3 + EC2
cloud-auditor fix --rollback                        # Undo last fix session
```

**CI/CD pipeline (NEW in v2.2.0)**
```bash
cloud-auditor scan --output sarif > results.sarif    # GitHub Security tab native
cloud-auditor scan --output json > findings.json     # Machine-readable for pipelines
cloud-auditor scan --fail-if-score-drops-by 10      # Fail build if score drops
```

---

## 6. Auto-Fix Engine (NEW in v2.2.0)
Cloud Auditor v2.2.0 introduces the auto-fix engine—the capability that fundamentally separates it from every evidence-only compliance tool including AWS Audit Manager. Every fix is reversible, previewed before application, and logged for auditing.

### 6.1 How It Works
1. `cloud-auditor fix` reads the most recent scan results from `web/scans/latest.json`.
2. For each qualifying finding, it maps the check ID to its corresponding dynamic fix logic.
3. In **dry-run mode**, it prints every action that would occur—nothing is changed.
4. In **apply mode**, it executes each fix via the AWS SDK.
5. Every change is logged to `~/.cloud-auditor/rollback.json` with the original resource state.
6. `cloud-auditor fix --rollback` reads that log and reverses changes in reverse order.

### 6.2 Fix Coverage by Service
| Service | Fixable Checks | Example Auto-Fix |
| :--- | :--- | :--- |
| **S3** | S3-001 to S3-005 | Block public access, enable encryption, enable versioning |
| **EC2** | EC2-001 to EC2-009 | Revoke open SSH/RDP, enforce IMDSv2, enable EBS encryption |
| **IAM** | IAM-002 to IAM-008 | Delete root access keys, rotate old keys, fix password policy |
| **RDS** | RDS-001 to RDS-006 | Disable public access, enable backups, enable Multi-AZ |
| **KMS** | KMS-001 to KMS-003 | Enable key rotation |
| **CloudTrail** | CT-001 to CT-003 | Enable trail, enable file validation, enable multi-region |
| **Secrets Mgr** | SM-001, SM-002 | Enable rotation, delete unused secrets (NEW in v2.2.0) |

### 6.3 Dry-Run Output Example
```bash
$ cloud-auditor fix --dry-run --severity critical

DRY RUN MODE: No changes will be applied
Found 3 critical findings to fix:

[1/3] S3-001: Public Access Block Missing on bucket: my-prod-bucket
#  Would run: aws s3api put-public-access-block --bucket my-prod-bucket \
#    --public-access-block-configuration '{"BlockPublicAcls":true,...}'

[2/3] EC2-001: SSH Port 22 Open to Internet on sg-0abc1234
#  Would run: aws ec2 revoke-security-group-ingress --group-id sg-0abc1234 \
#    --protocol tcp --port 22 --cidr 0.0.0.0/0

[3/3] IAM-002: Root Account Has Access Keys
#  Would run: aws iam delete-access-key --access-key-id AKIA...

Run without --dry-run to apply all 3 fixes.
```

---

## 7. CI/CD & DevOps Integration (NEW in v2.2.0)
Cloud Auditor v2.2.0 is the first local AWS security tool with native CI/CD integration. It can run in any pipeline, block deploys on new critical findings, and post results directly to GitHub's Security tab.

### 7.1 GitHub Actions
**Basic scan on every push**
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

**Advanced: fail PR if regressions introduced**
```yaml
      - name: Score-Delta Gate
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        run: cloud-auditor scan --fail-if-score-drops-by 5 --output json
        # Exits with code 1 if security score drops by 5+ points
```

---

## 8. Security Checks (120+ Total)
### 8.1 New Services Added in v2.2.0
| Service | Checks | Key Findings Covered |
| :--- | :--- | :--- |
| **WAF** | 8 | Rules enabled, logging on, rate limiting configured, SQLi/XSS rules |
| **Secrets Manager** | 6 | Rotation enabled, unused secrets, plaintext secrets in env vars |
| **ACM** | 7 | Expiring certs (<30 days), expired certs, wildcard cert usage |
| **ElastiCache** | 6 | Encryption in-transit/at-rest, Redis AUTH disabled |
| **OpenSearch** | 6 | VPC placement, public access policies, node-to-node encryption |
| **AWS Config** | 5 | Recorder not enabled, delivery channel missing, rules not deployed |

---

## 9. Compliance Frameworks
| Framework | Checks | Tier | Status |
| :--- | :--- | :--- | :--- |
| **CIS v2.0** | 45+ | **FREE** | Existing |
| **SOC 2** | 55+ | **ENTERPRISE** | Existing |
| **HIPAA** | 45+ | **ENTERPRISE** | Existing |
| **ISO 27001** | 55+ | **ENTERPRISE** | Existing |
| **PCI DSS v4.0** | 40+ | **ENTERPRISE** | **NEW** |

---

## 10. Dashboard Guide (v2.2.0 Enhanced)
URL: `http://localhost:3001/findings-dashboard` auto-opens after every scan.

### 10.1 New Dashboard Features in v2.2.0
- **Inline fix commands**: Every finding row shows its `aws-cli` fix command for instant copying.
- **Score trend line**: Line chart tracking your security score across the last 10 scans.
- **Fix-it checklist mode**: Mark findings as in-progress or resolved (persists between sessions).
- **Executive summary card**: 30-second management briefing with top risks and score deltas.
- **One-click branded PDF**: Generate professional reports directly from the UI.

---

## 11. Slack & Teams Alerts (NEW in v2.2.0)
Cloud Auditor can send webhook notifications when new **CRITICAL** or **HIGH** findings are detected.

### 11.1 Configuration Example (`config.json`)
```json
{
  "slack_webhook": "https://hooks.slack.com/services/...",
  "alert_on_severity": ["critical", "high"],
  "alert_mode": "new_only"
}
```

---

## 12. Multi-Region Scanning (NEW in v2.2.0)
v2.2.0 introduces parallel multi-region scanning using Go goroutines.
```bash
cloud-auditor scan --all-regions
```
The dashboard shows an aggregate score plus a per-region breakdown. Scans all 20+ AWS regions in parallel for a unified compliance view.

---

## 13. LocalStack Sandbox Testing
Test Cloud Auditor including the auto-fix engine without a real AWS account using LocalStack.
```bash
export AWS_ENDPOINT_URL=http://localhost:4566
cloud-auditor scan --region us-east-1
```

---

## 14. Architecture & Security Model
### 14.1 Security Model
Cloud Auditor **NEVER**:
- Stores AWS credentials to disk.
- Sends resource names or findings to external servers.
- Uploads scan results.
- Makes write calls unless `cloud-auditor fix` is explicitly invoked.

What the license server receives: **SHA-256 machine fingerprint + scan timestamp + security score number**. That is all.

---

## 15. Troubleshooting & FAQ
### 15.1 FAQ
**Q: Will Cloud Auditor modify my AWS resources without asking?**
No. Scans are 100% read-only. The fix engine only runs when you explicitly invoke `cloud-auditor fix`, and dry-run is the default.

**Q: Can I use it in CI/CD pipelines?**
Yes. Use `--output sarif` for GitHub Security tab integration or `--output json` for custom pipelines.

**Q: What happens after my 1-week Enterprise trial?**
Your account reverts to the Free tier automatically. All scan history is preserved. Upgrade anytime from `cloudauditor.vercel.app`.

---

[**Dashboard**](https://cloudauditor.vercel.app) | [**GitHub**](https://github.com/jenilrupapara001/Cloud-Auditor) | [**Releases**](https://github.com/jenilrupapara001/Cloud-Auditor/releases)

© 2026 Cloud Auditor. Built for the privacy-conscious cloud.
