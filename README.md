# **Multi Request Forgery** – AI‑Powered Fuzzer for 0‑Day Discovery  
*Licence • [MIT](LICENSE)  |  Author • Haroon Ahmad Awan (CyberZeus)  |  Date • 2025‑04‑21*

---

## Download the full pdf here
https://cyberzeus.pk/Multi_Request_Forgeries_MRF_AI_Powered_Web_Attack_Fuzzing_for_0_Day_Discovery.pdf

---

## Overview

- Uses **AI models** to assess threat likelihood: *Confirmed / Suspected*
- Enhances exposure detection accuracy with:
  - **AI threat tags**
  - **Confidence score (0‑1)** and explanation
  - Human clarifier output (e.g. “Check dnslog.cn panel”)
- Built‑in **blind SSRF beaconing** via `dnslog.cn`
- **AI‑adaptive stealth pacing** to evade WAFs / rate limits (`--stealth` on by default)

## Crawling

- Detects and parses:
  - Same‑domain hyperlinks (`<a href>`)
  - HTML forms (GET/POST)
  - JavaScript endpoints (`fetch`, `axios`, `XHR`)
- Outputs to a clean Markdown report → `sxc_findings.md`

---

## Feature Matrix

### 🧭 **Crawler Engine**
- Crawls links, forms, and JavaScript-defined endpoints  
- Honors page limit via `--max-pages`

### 🔁 **Multi-Request Forgery Engines**  
Includes novel request forgery chains mapped to **STRIDE** categories:

| Technique | Description | STRIDE Tags |
|----------|-------------|-------------|
| **SSRF** | Server-Side Request Forgery | Info Disclosure, Priv Esc |
| **CSRF/XSRF** | Cross-Site Request Forgery | Tampering, Repudiation |
| **MARSF** | Meta App Request Smuggling Forgery | Chain Exploit, Priv Injection |
| **RARF** | Recursive / Rebound SSRF | DNS Rebind, Alias SSRF |
| **VREF** | Verifier Request Forgery | IDOR, Priv Esc |
| **SREF** | Stored Request Forgery | Stored Abuse |
| **CLRF** | Client-Logic Request Forgery | CORS Bypass, Auth Leak |
| **EPRF** | Endpoint Relay Forgery | Message Hijack |
| **IMRF** | Interface Manipulation Request Forgery | DOM Tamper, UI Forgery |
| **UDRF** | Upstream Dependency Request Forgery | SDK Abuse |

### 🌐 **SSRF Engine**
- Probes:
  - Internal IPs (`127.0.0.1`, `169.254.*.*`)
  - Cloud metadata (`http://169.254.169.254/`)
  - Kubernetes DNS
  - `gopher://`, `file://`, and FTP schemes
- Detects blind SSRF via DNS beaconing

### 🛡️ **CSRF/XSRF Engine**
- Auto‑generates and submits:
  - GET/POST/iframe/fetch/anchor‑based requests
- Applies token‑removal and `text/plain` tricks
- Verifies actions via headless Firefox

### 🤖 **AI‑Stealth Engine**
- Intelligent request pacing based on HTTP response class
  - Slower for suspicious patterns (e.g., many 403s)
- Toggle using `--no-stealth`

### 📄 **Reporting**
- Outputs:
  - Markdown table with:
    - URL
    - Forgery type
    - STRIDE tags
    - Confidence score (0–1)
    - Confirmation status
    - Reason/explanation

### ⚙️ **Multithreaded Engine**
- Run requests in parallel  
- Threads adjustable via `--threads` (default: 14)

---

## Install & Run

```bash
git clone https://github.com/haroonawanofficial/sxc.git
cd sxc
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt        # requests, bs4, fake-useragent, playwright
playwright install firefox             # one-time setup
