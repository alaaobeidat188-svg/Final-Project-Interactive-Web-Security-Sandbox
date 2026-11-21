# Ghurir: Interactive Web Security Sandbox

A beginner-friendly website with three interactive security labs.
In each lab you press a payload, watch the vulnerability happen, then switch to the fixed version and see the same payload blocked.

## 🔗 Live Demo

**https://alaaobeidat188-svg.github.io/Final-Project-Interactive-Web-Security-Sandbox/**

Repository: https://github.com/alaaobeidat188-svg/Final-Project-Interactive-Web-Security-Sandbox

## 🧪 The Labs

| # | Lab | OWASP Category | CWE | Level |
|---|-----|----------------|-----|-------|
| 1 | Reverse Tabnabbing | A01: Broken Access Control | CWE-1022 | Easy |
| 2 | CSV Injection | A03: Injection | CWE-1236 | Medium |
| 3 | Insecure postMessage | A01: Broken Access Control | CWE-346 | Hard (team challenge) |

Each lab page contains: **What it is** · **The line** · **Try it** · **Why it matters** · **The fix** · **Sources**, plus a Vulnerable / Fixed switch.

---

### 1. Reverse Tabnabbing

**The bug:** a link that opens with `target="_blank"` but without `rel="noopener"` gives the new page access to `window.opener`.
**The vulnerable line:** `<a href="..." target="_blank">` with no `rel` attribute.
**Payloads:** *Inspect window.opener* and *Redirect the original tab* (the original tab turns into a fake login page).
**The fix:** `rel="noopener noreferrer"`. The same payloads are blocked because `window.opener` is `null`.

### 2. CSV Injection

**The bug:** a customer name that starts with `=`, `+`, `-` or `@` is exported to a CSV file unchanged, and a spreadsheet may treat it as a formula.
**The vulnerable line:** the export function writes the raw cell value (`const name = c.name;`).
**Payloads:** `=HYPERLINK(...)` (shows a blue link that opens the local simulated page `attacker.html`) and `=1+1`. A built-in simulated spreadsheet shows what would be evaluated, and the harmless `report.csv` can be downloaded.
**The fix:** prefix risky values with a single quote so they are treated as plain text. The same payloads are shown as text.

### 3. Insecure postMessage (team challenge)

**The bug:** a `message` listener that never checks `event.origin` answers any window, and replies with target `"*"`.
**The vulnerable line:** the handler has no check of `e.origin` before it sends the session token.
**Payloads:** *steal the session token* from `https://evil.example`, and a *look-alike origin* `https://bank.example.evil.com`.
**The fix:** check `event.origin` against an exact allowlist and reply only to `e.origin`. The same messages are blocked.

---

## 🛡️ Safety

- All demos are **client-side simulations**.
- No backend, no login, no database.
- No real passwords, personal data, or company logos.
- No real malicious code is run, and no real site is ever contacted.

## 🛠️ Tech Stack

HTML, CSS and JavaScript only. No frameworks.

## 📁 Project Structure

```
.
├── index.html
├── tabnabbing.html
├── csv-injection.html
├── postmessage.html
├── attacker.html
├── css/
│   └── style.css
├── js/
│   ├── lab.js
│   ├── tabnabbing.js
│   ├── csv-injection.js
│   └── postmessage.js
└── README.md
```

> Keep the folders next to the HTML files, or the pages lose their style and scripts.

## 🚀 Run Locally

```bash
git clone https://github.com/alaaobeidat188-svg/Final-Project-Interactive-Web-Security-Sandbox.git
cd Final-Project-Interactive-Web-Security-Sandbox
# open index.html in your browser
```

## 👥 Team

- Alaa Obeidat
- Rand Almoghier
- Rania Alassouli
- Hamza Almoahammd
- Yousef Shalakhti

## 📚 Sources

- Reverse Tabnabbing: [OWASP](https://owasp.org/www-community/attacks/Reverse_Tabnabbing) · [CWE-1022](https://cwe.mitre.org/data/definitions/1022.html)
- CSV Injection: [OWASP](https://owasp.org/www-community/attacks/CSV_Injection) · [CWE-1236](https://cwe.mitre.org/data/definitions/1236.html)
- Insecure postMessage: [OWASP: Testing Web Messaging](https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/11-Client-side_Testing/11-Testing_Web_Messaging) · [CWE-346](https://cwe.mitre.org/data/definitions/346.html)

---

*42 Irbid, Final Project, November 2026*
