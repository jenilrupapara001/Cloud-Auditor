# Installation Guide

Cloud Auditor is distributed as a pre-compiled, hardened binary. No Go installation is required on your system.

## 🚀 Quick Download

1. Go to the [Releases](https://github.com/USER/cloud-auditor/releases) page.
2. Download the version corresponding to your Operating System and Architecture:
   - **macOS (Intel)**: `cloud-auditor-darwin-amd64`
   - **macOS (Apple Silicon)**: `cloud-auditor-darwin-arm64`
   - **Linux**: `cloud-auditor-linux-amd64`
   - **Windows**: `cloud-auditor-windows-amd64.exe`

## 🛠️ Setup Instructions

### macOS / Linux

```bash
# Move to a directory in your PATH (optional)
mv ~/Downloads/cloud-auditor-darwin-arm64 /usr/local/bin/cloud-auditor

# Grant execution permissions
chmod +x /usr/local/bin/cloud-auditor

# Verify installation
cloud-auditor --version
```

### Windows

1. Download the `.exe` file.
2. Add the folder containing the `.exe` to your System PATH environment variable.
3. Open PowerShell or Command Prompt and run `cloud-auditor.exe --version`.

## 🔐 Verifying the Binary

Every release includes a `checksums.txt` file. We recommend verifying the SHA256 hash of your download:

```bash
# example
shasum -a 256 cloud-auditor-darwin-arm64
```

Compare the output with the hash provided in the release notes.
