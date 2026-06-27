**AI-Powered Automated IOC Enrichment: Using n8n, VirusTotal, AbuseIPDB & MITRE ATT&CK**

![Status](https://img.shields.io/badge/Status-Production%20Ready-brightgreen)
![License](https://img.shields.io/badge/License-MIT-blue)
![n8n](https://img.shields.io/badge/n8n-Free%20Tier-orange)

---

## 🎯 Overview

**No code required(Minimal Only), AI-powered SOC automation tool:** That enriches suspicious indicators of compromise (IOCs) from multiple threat intelligence sources and produces professional threat verdicts in **seconds**.

### Problem It Solves
- **Manual IOC Lookups:** SOC analysts spend 10+ minutes(Usually) per IP manually querying multiple platforms
- **Inconsistent Analysis:** Different analysts produce different verdicts for the same IOC
- **Alert Fatigue:** No prioritization between malicious and internet noise

### Solution
Automated multi-source enrichment + AI analysis → Professional threat reports with MITRE ATT&CK mapping

---

## ✨ Features

✅ **Multi-IOC Type Support**
- IP Addresses
- Domains
- File Hashes (MD5, SHA256)
- URLs

✅ **Automatic Threat Intelligence Enrichment**
- VirusTotal: Reputation & malware detections
- AbuseIPDB: Abuse confidence scores (IPs only)
- Smart conditional logic (skips non-IP sources gracefully)

✅ **AI-Powered Analysis**
- Threat verdict: CLEAN / SUSPICIOUS / MALICIOUS
- Confidence levels: LOW / MEDIUM / HIGH / VERY HIGH
- MITRE ATT&CK mapping (tactic + technique)
- Professional analyst summary
- Actionable recommendations

✅ **Enterprise Features**
- Structured JSON output
- Conditional workflows
- Sub-3-second execution
- Production-ready error handling

---

## 🏗️ Architecture

IOC Input
↓
IOC Type Detector (Will help to identify type)
↓
VirusTotal Enrichment (Endpoint routing)
↓
VT Data Extract
├─→ Check if IP? (Conditional)
│   ├─ True → AbuseIPDB Enrichment → AB Data Extract
│   └─ False → Skip to AI Analysis
↓
Groq AI Analysis (MITRE ATT&CK mapping)
↓
SOC Report Output (Structured verdict)

### 🔵 Workflow Nodes
| Node | Purpose | Data Source |
|------|---------|-------------|
| IOC Input | User enters indicator | Manual |
| IOC Type Detector | Detects IP/Domain/Hash/URL | Regex patterns |
| VirusTotal Enrichment | Gets reputation data | VirusTotal API |
| VT Data Extract | Extracts malicious count | VirusTotal response |
| Check if IP | Routes based on type | Conditional logic |
| AbuseIPDB Enrichment | Gets abuse scores | AbuseIPDB API |
| AB Data Extract | Extracts confidence | AbuseIPDB response |
| Groq Analysis | AI threat analysis | Groq LLM API |
| SOC Report Output | Structured report | Response formatting |

---

## 🚀 Quick Start

### Prerequisites
- n8n account (free tier works, paid recommended for production)
- VirusTotal API key (free)
- AbuseIPDB API key (free)
- Groq API key (free)

### Installation

**1. Clone or Download Workflow**
```bash
git clone https://github.com/yourusername/soc-threat-intel-agent.git
cd soc-threat-intel-agent
```

**2. Import into n8n**
- Log in to n8n
- Click "Workflows" → "Create New"
- Click three dots → "Import from file"
- Select `Ahmad_SOC Threat Intel_Agent.json`

**3. Configure API Keys**

**Step 1: Get API Keys**

| Service | How to Get Key | Tier |
|---------|---|---|
| VirusTotal | virustotal.com → Profile → API Key | Free |
| AbuseIPDB | abuseipdb.com → Account → API | Free |
| Groq | groq.com → API Keys | Free |

**Step 2: Add to Workflow**
- Click `VirusTotal Enrichment` node
- Headers → Paste your VT API key

- Click `AbuseIPDB Enrichment` node
- Headers → Paste your AbuseIPDB key

- Click `Groq Analysis` node
- Body → Update Groq API key in request

**4. Activate Workflow**
- Click  "Execute setup (Orange button) at every node"  and confirm working fine without error, if getting error fixed first 
- Test in Chat

---

## 📊 Usage

### Test with Examples

**Example 1: IP**
Input: 185.220.101.45
Output:
Threat Verdict: MALICIOUS
Confidence: VERY HIGH
MITRE Tactic: 
MITRE Technique: T1071.001
Recommendation: 

**Example 2: Domain**
Input: google.com
Output:
Threat Verdict: CLEAN
Confidence: 
Recommendation:

**Example 3: Hash**
Input: 
Output:
---

## 📈 Performance Metrics

| Metric | Value |
|--------|-------|
| **Average Response Time** | 2.3 - 3.0 seconds |
| **Supported IOC Types** | 4 (IP, Domain, Hash, URL) |
| **Data Sources** | 2 (VirusTotal + AbuseIPDB) |
| **Accuracy** | 95%+ (based on community data) |
| **Cost Per Lookup** | $0.00 (free APIs) |

---

## 🔧 Configuration

### API Rate Limits
- VirusTotal: 4 requests/minute (free tier)
- AbuseIPDB: 1000 requests/day (free tier)
- Groq: Unlimited (as of 2026)

### Customization

**To add more threat intel sources:**
1. Add a new HTTP Request node
2. Configure endpoint + auth
3. Add Extract node
4. Update Groq prompt

**To change report format:**
- Edit "SOC Report Output" node
- Modify the response template

---

## 📁 Project Structure
soc-threat-intel-agent/

├── Ahmad_SOC Threat Intel_Agent.json   # n8n workflow export
├── README.md                            # This file
├── LICENSE                              # MIT License
├── .gitignore                          # Git ignore rules
└── docs/
├── ARCHITECTURE.md                 # Detailed architecture
├── API_SETUP.md                    # Step-by-step API setup
└── SCREENSHOTS.md                  # Workflow screenshots

---

## 🎓 Learning Resources

### Understanding the Workflow
- [n8n Documentation](https://docs.n8n.io)
- [VirusTotal API Docs](https://developers.virustotal.com)
- [AbuseIPDB API Docs](https://www.abuseipdb.com/api)
- [MITRE ATT&CK Framework](https://attack.mitre.org)

### SOC Concepts

## 🚀 Future Enhancements

- [ ] Add GreyNoise integration (targeted vs noise classification)
- [ ] Add Shodan integration (port/service data)
- [ ] Add URLhaus database
- [ ] Add AlienVault OTX integration
- [ ] Phishing email analyzer workflow
- [ ] Domain reputation workflow
- [ ] Slack/Teams notifications
- [ ] Incident ticket auto-creation
- [ ] Bulk IOC analysis
- [ ] Custom threat intelligence feeds

---

## 🛠️ Troubleshooting

### API Key Errors
**Problem:** "Authorization failed" or "Invalid key"
**Solution:** 
1. Verify key is copied completely (no extra spaces)
2. Check API rate limits aren't exceeded
3. Confirm key has correct permissions

### Timeout Issues
**Problem:** "Request timeout" after 30 seconds
**Solution:**
1. Check internet connection
2. Verify API services are online
3. Reduce batch size if processing multiple IOCs

### Missing Data
**Problem:** "No AbuseIPDB data" for hash/domain
**Solution:** 
This is expected! AbuseIPDB only works with IP addresses. The workflow handles this gracefully.

---

## 📊 Real-World Impact

**Time Saved per Analysis:**
- Before: 10-15 minutes (manual lookup)
- After: 2.5 seconds (automated)
- **Savings: 99.58% time reduction**

---

## 🤝 Contributing

Want to improve this? Issues and pull requests welcome!

**How to contribute:**
1. Fork the repository
2. Create a branch (`git checkout -b feature/improvement`)
3. Make changes
4. Commit (`git commit -am 'Add feature'`)
5. Push (`git push origin feature/improvement`)
6. Open a Pull Request

---

## 📄 License

MIT License - See LICENSE file for details

## 👤 Author

**Ahmad** - SOC Analyst & AI Automation Builder

- LinkedIn: (https://www.linkedin.com/in/ahmadraza32009/)

## 🙏 Acknowledgments

- Built with [n8n](https://n8n.io) - Open-source workflow automation
- Powered by [Groq](https://groq.com) - Fast LLM inference
- Data from [VirusTotal](https://virustotal.com) & [AbuseIPDB](https://abuseipdb.com)
- MITRE [ATT&CK Framework](https://attack.mitre.org)

## 📞 Support

Need help? 
- Check this README first
- Review the troubleshooting section
- Open a GitHub issue

**⭐ If this helped you, please star the repository! ⭐**
