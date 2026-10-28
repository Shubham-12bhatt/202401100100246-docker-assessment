# FestPass 2026 — Docker & Container Security Assessment

## Student Details

- **Name:** Shubham Bhatt
- **Registration Number:** 202401100100246
- **Application Port:** 8046
- **Docker Hub Username:** zoro69bhatt
- **Docker Hub Repository:** https://hub.docker.com/r/zoro69bhatt/fest-backend

## AI Tools Used

- **ChatGPT:** Used for understanding Docker assessment requirements, troubleshooting Docker and PowerShell commands, Docker Compose configuration, Trivy security scanning, Docker Hub image publishing, Cosign signing and verification, and Git workflow guidance.

## Incomplete Steps

- None. All Stage 1–5 tasks were completed.

## Stage 3 — Container Security Scanning

### Trivy Vulnerability Comparison

| Metric                   | Before (fest-backend:0.1) | After (fest-backend:0.2) |
| ------------------------ | ------------------------- | ------------------------ |
| HIGH Vulnerabilities     | 2249                      | 49                       |
| CRITICAL Vulnerabilities | 234                       | 0                        |
| Docker Image Disk Usage  | 1.61 GB                   | 219 MB                   |

### Security Improvements

- Updated Python base image to python:3.13-slim.
- Upgraded Flask, Werkzeug, and other Python dependencies.
- Configured the backend container to run as a non-root user.
- Reduced HIGH vulnerabilities by approximately 97.8%.
- Reduced CRITICAL vulnerabilities from 234 to 0.
- Reduced Docker image disk usage by approximately 86%.

### Security Verification

Command:
`trivy image --severity CRITICAL --ignore-unfixed --exit-code 1 fest-backend:0.2`

Exit code: `0` (Passed)

### Evidence

- Initial scan: `reports/trivy-before.txt`
- Updated scan: `reports/trivy-after.txt`
- Initial screenshot: `screenshots/S3-1.png`
- Final screenshot: `screenshots/S3-3.png`

## Stage 4 — Docker Hub Release

Docker Hub Repository: https://hub.docker.com/r/zoro69bhatt/fest-backend

### Published Image Tags

- `zoro69bhatt/fest-backend:1.0.0`
- `zoro69bhatt/fest-backend:1.0`

### Version 1.0.0 Digest

`sha256:b86609bbe1eed77d1460461147bc70895b5feec615ad5a16c57b4a8371384c94`

Both tags reference the same Docker image.

### Evidence

- `screenshots/S4-1.png` — Successful Docker Hub pushes and digests.
- `screenshots/S4-2.png` — Docker Hub repository Tags page.


## Stage 5 — Cosign Image Signing and Verification

### 5.1 — Key Generation

Generated a password-protected Cosign key pair.

- Public key: `cosign.pub`
- Private key: `cosign.key` (excluded from Git using `*.key` in `.gitignore`)

### 5.2 — Sign Version 1.0.0

Signed the published Docker image using its immutable digest.

- Image: `zoro69bhatt/fest-backend:1.0.0`
- Digest: `sha256:b86609bbe1eed77d1460461147bc70895b5feec615ad5a16c57b4a8371384c94`

### 5.3 — Signature Verification

Verified the signed image using `cosign.pub`.

Verification confirmed:
- Cosign claims were validated.
- Transparency log evidence was verified.
- Signature matched the public key.

### 5.4 — Unsigned Image Verification Test

Published `zoro69bhatt/fest-backend:1.0.1` without signing it.

- Digest: `sha256:d45c9b70c6cc69b8b546d0d2fa602460cea96d1fb885a2c468bb798f816d8c4f`
- Verification result: `Error: no signatures found`
- Exit code: `10` (expected failure)

### Evidence

- `screenshots/S5-1.png` — Password-protected key generation.
- `screenshots/S5-2.png` — Signing version 1.0.0 by digest.
- `screenshots/S5-3.png` — Successful signature verification.
- `screenshots/S5-4.png` — Expected verification failure for unsigned version 1.0.1.
