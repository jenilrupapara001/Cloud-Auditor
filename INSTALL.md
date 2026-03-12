<div align="center">

```
 ██████╗██╗      ██████╗ ██╗   ██╗██████╗      █████╗ ██╗   ██╗██████╗ ██╗████████╗ ██████╗ ██████╗
██╔════╝██║     ██╔═══██╗██║   ██║██╔══██╗    ██╔══██╗██║   ██║██╔══██╗██║╚══██╔══╝██╔═══██╗██╔══██╗
██║     ██║     ██║   ██║██║   ██║██║  ██║    ███████║██║   ██║██║  ██║██║   ██║   ██║   ██║██████╔╝
██║     ██║     ██║   ██║██║   ██║██║  ██║    ██╔══██║██║   ██║██║  ██║██║   ██║   ██║   ██║██╔══██╗
╚██████╗███████╗╚██████╔╝╚██████╔╝██████╔╝    ██║  ██║╚██████╔╝██████╔╝██║  ██║   ╚██████╔╝██║  ██╗
 ╚═════╝╚══════╝ ╚═════╝  ╚═════╝ ╚═════╝     ╚═╝  ╚═╝ ╚═════╝ ╚═════╝ ╚═╝   ╚═╝    ╚═════╝ ╚═╝  ╚═╝
```

**Zero-Trust AWS Security & Compliance Auditing · Version 2.1.0 · 2026**

</div>

---

## 📦 Installation guide

### macOS (Intel & Apple Silicon)
```bash
# Download (Apple Silicon M1/M2/M3/M4)
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.1.0/cloud-auditor-darwin-arm64 -o cloud-auditor

# OR Download (Intel)
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.1.0/cloud-auditor-darwin-amd64 -o cloud-auditor

# Make executable
chmod +x cloud-auditor

# Scan
./cloud-auditor scan --region us-east-1
```

### Linux (AMD64)
```bash
curl -L https://github.com/jenilrupapara001/Cloud-Auditor/releases/download/v2.1.0/cloud-auditor-linux-amd64 -o cloud-auditor
chmod +x cloud-auditor
./cloud-auditor scan --region us-east-1
```

### Windows (AMD64)
1. Download `cloud-auditor-windows-amd64.exe` from [Releases](https://github.com/jenilrupapara001/Cloud-Auditor/releases).
2. Open PowerShell and navigate to the download folder.
3. Run: `./cloud-auditor-windows-amd64.exe scan --region us-east-1`

---

## 🔑 AWS Prerequisites
Your IAM user/role needs the **`ReadOnlyAccess`** managed policy. No write permissions are ever required.

---

<div align="center">

**[cloudauditor.io](https://cloudauditor.io)** · [Releases](https://github.com/jenilrupapara001/Cloud-Auditor/releases)

</div>
