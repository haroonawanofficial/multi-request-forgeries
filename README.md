# **Multi Request Forgery** AI Powered Fuzzer for 0 Day Discovery
*Licence • [MIT](LICENSE)  |  Author • Haroon Ahmad Awan (CyberZeus)  |  Date • 2025‑04‑21*


---

## Overview

- Provides full awareness of it is hit or suspected using AI Models
- Better Exposure
- Better Confidence
- Adds per‑finding:
  - AI threat tags  
  - **Confidence score** + *Confirmed / Suspected* status.  
  - Human clarifier (e.g. “Check dnslog.cn panel”).  
- Built‑in **dnslog.cn** beacon payloads for blind SSRF.  
- **AI‑style adaptive pacing** (`--stealth` on by default) evades WAF / rate limits.  

# Crawls:
  - Same‑domain links (`<a href>`).  
  - HTML forms.  
  - JS‑defined `fetch() / axios / XHR` URLs.  

# Generates one tidy Markdown report → `sxc_findings.md`.

---

## Feature matrix

- **Crawler**  
  - Walks links / forms / JS endpoints.  
  - Obeys `--max-pages` cap.  

- **SSRF engine**  
  - Internal IPs, AWS metadata, k8s DNS, `gopher://`, `file://`.  
  - Blind beacon via **dnslog.cn**.  
  - Confidence weighting from reflection or content heuristics.  

- **CSRF / XSRF engine**  
  - Auto‑submitting POST / GET / iframe / fetch payloads.  
  - Token‑stripping (`text/plain`) tricks.  
  - Headless Firefox verification.  

- **AI Stealth**  
  - Adaptive delays for 2xx / 3xx / 4xx‑5xx.  
  - Toggle with `--no-stealth`.  

- **Reporting**  
  - Markdown lines with STRIDE tags, confidence 0‑1, status & reason.  

- **Multithreaded**  
  - `--threads` (default 14) runs endpoints in parallel.  

---

## Install & run

```bash
git clone https://github.com/haroonawanofficial/sxc.git
cd sxc
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt        # requests, bs4, fake-useragent, playwright
playwright install firefox             # one‑time headless driver
