
## Stage 3 — Container Security Scanning

### Trivy Vulnerability Comparison

| Metric | Before (fest-backend:0.1) | After (fest-backend:0.2) |
|---|---|---|
| HIGH Vulnerabilities | 2249 | 49 |
| CRITICAL Vulnerabilities | 234 | 0 |
| Docker Image Disk Usage | 1.61 GB | 219 MB |

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
  