# 🛡️ PhishGuard — AI Phishing Email Analyzer

> Forensic-grade phishing detection in the browser. Paste a raw email, get a full threat report — header authentication, URL scanning, AI reasoning, MITRE ATT&CK mapping, scan history, and a full phishing education hub. Nothing ever leaves your device.

![PhishGuard](https://img.shields.io/badge/PhishGuard-v2.0-f0c060?style=for-the-badge&logo=shield&logoColor=black)
![HTML](https://img.shields.io/badge/HTML-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![AI](https://img.shields.io/badge/AI-Groq_LLaMA--3-ff6b35?style=for-the-badge)
![No Backend](https://img.shields.io/badge/No_Backend-Client_Side_Only-39ff14?style=for-the-badge)

---

## 🖥️ Live Demo

👉 **[Try it here](https://tryphishguard.netlify.app/)**

---

## ✨ Features

### 🔬 Analyze Tab
- **7 forensic modules** — headers, spoofing, URLs, urgency, attachments, AI, and MITRE mapping run in sequence with a live progress tracker
- **Header authentication** — extracts SPF, DKIM, and DMARC status, detects Reply-To mismatches and suspicious mailer strings
- **Sender spoofing detection** — catches brand impersonation, typosquatted domains, suspicious keywords, and high-risk TLDs (`.ru`, `.xyz`, `.tk`)
- **URL scanner** — extracts every link and scores each for brand impersonation, IP address URLs, deep subdomains, and suspicious query parameters
- **Urgency & manipulation detector** — scans for 15+ psychological pressure phrases used in social engineering
- **Attachment risk scoring** — flags dangerous file types like `.exe`, `.ps1`, `.js`, `.vbs`, `.hta`, and more
- **AI deep analysis** — Groq AI reasons over all findings and produces a structured threat verdict
- **MITRE ATT&CK mapping** — maps detected behaviors to real techniques (T1566, T1598, T1036, T1204, T1189)
- **Confidence score** — 0–100 phishing probability with weighted scoring across all modules

### 🕘 History Tab
- Every scan is saved to **localStorage** with timestamp, sender domain, score, and verdict
- Persists across browser sessions — your scan history survives page refreshes and restarts
- One-click clear to wipe all history

### 📚 Learn Tab
- **By the numbers** — 4 live phishing statistics (3.4B emails/day, 36% of breaches, $4.9M avg breach cost, 97% of users can't spot a phish)
- **Attack type breakdown** — Phishing, Spearphishing, Whaling, Clone Phishing, Smishing, Vishing, Quishing, and BEC explained
- **Red flags checklist** — 8 practical indicators to spot a phishing email
- **Psychological tactics** — Authority, Urgency, Fear, and Familiarity explained
- **Technical tricks** — Typosquatting, Homograph attacks, Subdomain abuse, and Link shorteners

### ⚙️ Settings Tab
- **Alert threshold slider** — set your own sensitivity from 10–90% with dynamic labels (Very Sensitive → Low Sensitivity)
- **Monitoring toggles** — clipboard URL monitoring, auto-scan on link click
- **Phishing database toggles** — PhishTank, Google Safe Browsing, Local Heuristics
- **API key manager** — save your Groq key once, syncs with the Analyze tab automatically
- **Clear all data** — wipe history, API key, and settings from localStorage in one click
- All settings **persist across sessions** via localStorage

---

## 🧠 How It Works

### Scoring Model
Each module produces an independent 0–100 risk score. The final phishing probability is a weighted aggregate:

```
Score = (Headers × 0.20) + (Spoofing × 0.25) + (Urgency × 0.20) + (URLs × 0.20) + (Attachments × 0.15)
```

Spoofing and URLs carry the highest weight — they're the most reliable real-world phishing indicators.

### Header Authentication
Parses raw RFC 2822 headers and extracts authentication results from the `Authentication-Results` field. SPF, DKIM, and DMARC are each checked and scored independently.

### Sender Spoofing
Compares the display name against the actual sending domain. Checks for 10+ major brands. Scans the domain for embedded keywords. Cross-references the TLD against a blocklist of 9 high-abuse extensions.

### URL Analysis
Extracts all URLs with regex, deduplicates, and runs each through 6 checks: TLD risk, hostname brand impersonation, IP address usage, subdomain depth, URL length, and suspicious query parameters.

### AI Analysis
Sends a structured summary of all module findings plus the first 1,200 characters of the email to `llama-3.1-8b-instant` via Groq. Returns a structured forensic verdict: threat assessment, key indicators, attack vector, and recommended action. Optional — all other modules work fully offline.

---

## 🚀 Usage

No installation. No dependencies. No server.

```bash
# Clone and open
git clone https://github.com/tahahahaa/phishguard
cd phishguard
open phishguard.html
```

Or visit **[tryphishguard.netlify.app](https://tryphishguard.netlify.app)** — nothing to install.

---

## 🔑 Groq API Key (Optional)

Only required for the AI analysis module. All 6 other modules work completely offline.

1. Go to [console.groq.com](https://console.groq.com) and sign up — free, no credit card
2. Navigate to **API Keys → Create API Key**
3. Paste it in the Analyze tab or save it permanently in Settings
4. Your key goes directly to `api.groq.com` — nothing else ever sees it

---

## 📊 Verdict Thresholds

| Score | Verdict | Meaning |
|---|---|---|
| 0–14 | ✅ Clean | No significant indicators found |
| 15–39 | 🟡 Low Risk | Minor flags, likely benign |
| 40–59 | 🟠 Suspicious | Multiple red flags — verify before acting |
| 60–79 | 🔴 Likely Phishing | Strong indicators — treat as malicious |
| 80–100 | ☠️ Phishing | High-confidence threat |

---

## 🗡️ MITRE ATT&CK Coverage

| Technique | ID | Triggered By |
|---|---|---|
| Spearphishing Attachment | T1566.001 | Sender spoofing or header anomalies |
| Spearphishing Link | T1566.002 | Suspicious URLs detected |
| Phishing for Information | T1598 | Urgency and manipulation tactics |
| Masquerading: Match Legitimate Name | T1036.005 | Brand impersonation in display name |
| User Execution: Malicious File | T1204.002 | Dangerous attachment extension |
| Drive-by Compromise | T1189 | Redirect parameters in URLs |

---

## 🛡️ Security & Privacy

- **No backend** — zero server-side code
- **No transmission** — nothing leaves your browser except one optional call to `api.groq.com`
- **No tracking** — no analytics, no cookies, no telemetry
- **localStorage only** — scan history and settings stay on your device and nowhere else
- **No dependencies** — pure vanilla HTML/CSS/JS, no npm, no frameworks
- **Auditable** — the entire app is one HTML file you can read start to finish
- Safe to use with real emails

---

## 🗂️ Project Structure

```
phishguard.html    ← entire app in a single file (Analyze + History + Learn + Settings)
README.md          ← this file
LICENSE            ← MIT
```

---

## 🔧 Tech Stack

- **Vanilla JavaScript** — all analysis logic, no frameworks
- **HTML5 / CSS3** — Bricolage Grotesque + Outfit + JetBrains Mono
- **localStorage** — scan history and settings persistence
- **Groq API** — `llama-3.1-8b-instant` for AI deep analysis
- **No build tools, no npm, no dependencies**

---

## 👤 Author

**Muhammad Taha Sheikh**  
BS Cybersecurity · Karachi, Pakistan

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/tahahahaa)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:tahaahmed1877@gmail.com)

---

## 📄 License

MIT — free to use, modify, and distribute.

---

<div align="center">
<sub>// Forensic analysis. Zero trust. Nothing stored on any server.</sub>
</div>
