# OpenClaw Security Analysis & SecureClaw Roadmap

## 1. Top ClawHub Security Skills & Their Features

Based on the most downloaded security tools on ClawHub, the community is currently installing:

- **ClawDefender / MoltGuard:** Input sanitizers and runtime guardrails. They actively monitor for prompt injection, SSRF, and command injection.
- **Security Auditor:** Focuses on OWASP Top 10, scanning code and configuration for hardcoded secrets and poor validation.
- **Clawdbot Security Check:** An environment scanner that checks `~/.openclaw/openclaw.json` and system permissions to ensure the daemon isn't running with excessive privileges.

## 2. The Biggest OpenClaw Issues Right Now (From Recent Hacks & Forums)

Recent reports from Cisco, Kaspersky (CVE-2026-25253), Snyk, and Reddit highlight a massive security crisis for OpenClaw users:

- **The Toxic Supply Chain:** A staggering ~13-15% of community skills on ClawHub contain malicious payloads (credential theft, backdoors).
- **Indirect Prompt Injection via Chat:** Attackers are using link previews and malicious files in Telegram/Discord to inject commands into the bot's context.
- **Silent Data Exfiltration:** Malicious skills and injected prompts are tricking the bot into using `exec` or `web_fetch` to send workspace data and environment variables to external servers.
- **Browser Auth Bypass ("ClawJacked"):** The bot failing to distinguish between trusted local connections and malicious websites running in the user's browser, allowing zero-click CSRF takeovers.
- **Widespread Misconfigurations:** Over 40,000+ instances exposed to the internet because they bind to `0.0.0.0` without authentication by default.

## 3. The Blueprint for "SecureClaw"

To build the ultimate OpenClaw security skill, SecureClaw should aggregate these features into a single, cohesive runtime guardrail. Instead of users installing 4 different plugins that might conflict, SecureClaw directly addresses the panic around the "ToxicSkills" supply chain and the prompt injection vulnerabilities making headlines right now.

### A. Supply Chain Scanner (Pre-Execution)

Automatically scans newly installed skills and `SKILL.md` files for malicious payloads, hidden `exec` commands, and known toxic patterns before they are allowed to run.

### B. Chat Context Sanitizer (Input Guard)

Strips malicious indirect prompt injections from Telegram/Discord link previews, incoming emails, and fetched web pages.

### C. Exfiltration Blocker (Egress Control)

Monitors `exec` and `web_fetch` tool calls in real-time. If the agent attempts to send data to an unauthorized external IP or domain, SecureClaw blocks the action and alerts the user.

### D. Deployment Hardening (Config Audit)

A one-click `secureclaw --audit` command (or comprehensive checklist) that checks `~/.openclaw/openclaw.json` for proper sandboxing, removes overly permissive tool access, and enforces strict workspace boundaries.
