# 🔒 SECURITY.md — Anti-Crack & Hardening Deep Dive

Cloud Auditor is built with multiple layers of defense to protect its intellectual property and ensure that premium features remain exclusive to verified subscribers.

---

## 🛡️ The 6-Layer Defense Model (V2.1.0)

### 1. Cryptographic Response Signing (RSA-2048)
Every packet from the server is a JWS (JSON Web Signature) signed with a **Private RSA-2048 key**.
*   **The Mechanism**: The CLI checks every response against an **embedded Public RSA Key**. If the signature is missing or incorrect, the CLI reverts to the "Free" tier immediately.

### 2. Multi-Layer Hardware Binding (Anti-Share)
Licenses are machine-locked identities, protected against VM cloning.
*   **The Mechanism**: The CLI generates a `MachineID` based on a SHA-256 hash of **Motherboard UUID + CPU + MAC Addresses**.
*   **The Lockdown**: The server binds the API key to this unique hardware signature.

### 3. Anti-Replay Protection (Nonce & Expiry)
*   **Nonce**: Every request includes a unique UUID (Nonce). The server signs this nonce back into the response.
*   **24h Expiry**: JWT tokens expire every 24 hours, limiting the window of exposure for captured tokens.

### 4. Binary Integrity Self-Check (Anti-Patch)
*   **Self-Hash Verification**: At runtime, the CLI calculates its own SHA-256 hash and compares it to a value embedded at compile-time. If the binary has been hex-edited or patched, it will self-terminate.

### 5. MITM Protection (Certificate Pinning)
*   **Cert Pinning**: The CLI hard-codes the SHA-256 fingerprint of the server's TLS certificate, preventing interception via proxies like Charles or mitmproxy.
*   **TLS 1.3**: Only the latest, most secure transport protocol is permitted.

### 6. Binary Hardening & Obfuscation
*   **Symbol Stripping**: We use `-ldflags="-s -w"` to remove the symbol table and DWARF debug information.
*   **Static Linking**: All dependencies are baked into a single atomic binary.

---

## 🚦 Security Audit Workflow (V2.1.0)

1.  **Integrity**: CLI verifies its own binary hash.
2.  **Fingerprint**: CLI collects hardware IDs and generates a Nonce.
3.  **Auth**: CLI sends Key + Fingerprint + Nonce over pinned TLS 1.3.
4.  **Sign**: Server verifies key/machine binding and signs a 24h JWT with the Nonce.
5.  **Unlock**: CLI verifies RSA signature, Nonce, and Expiry before unlocking features.

---

## 🛠️ Security for Developers

*   **NEVER** commit `private.pem` or `binary.hash` to version control.
*   **ALWAYS** use the hardened build (`make build`) for production releases.
*   **AUDIT** the `internal/security` package whenever you modify fingerprinting or integrity logic.
