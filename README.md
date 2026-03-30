# SecureClaw Skill for ClawHub

**Instantly harden your OpenClaw instance with native security prompts and best practices.**

## Quick Start

```bash
# Global installation from this repository (enables the CLI command)
npm install -g .
# OR via ClawHub
clawhub install secureclaw
```

## What is SecureClaw?

SecureClaw is a single, cohesive runtime guardrail and zero-dependency skill that provides your OpenClaw agent with the necessary system prompts, boundary definitions, and best practices to defend against the most critical threats right now:

- **Supply Chain Scanner (Pre-Execution):** Stops the installation of toxic community skills by auditing code for malicious payloads and hidden `exec` commands before they run.
- **Chat Context Sanitizer (Input Guard):** Strips malicious indirect prompt injections from Telegram/Discord link previews, incoming emails, and fetched web pages.
- **Exfiltration Blocker (Egress Control):** Real-time monitoring of `exec` and `web_fetch` to ensure your workspace data and environment variables aren't leaked to malicious external endpoints.
- **Deployment Hardening (Config Audit):** A comprehensive checklist and the `secureclaw --audit` command to lock down `~/.openclaw/openclaw.json`, removing overly permissive tool access and enforcing strict sandboxing.
- **Role Manipulation / Jailbreaks:** Prevents attackers from making you "act as a hacker" or "enter developer mode."

It relies **entirely on your local LLM's reasoning** and does not send data to any 3rd party APIs.

## Included Guidelines

Once installed, SecureClaw integrates directly into your agent's system memory. It provides the following resources:

1. **`PROMPTS.md`**: Core system instructions to append to your agent's persona.
2. **`TOOL_SAFETY.md`**: Best practices for evaluating when and how to execute tools.
3. **`INCIDENT_RESPONSE.md`**: How the agent should respond when a security violation is detected.

## Why SecureClaw?

While powerful external scanners like ARGUS can provide deep on-chain risk assessments and sophisticated threat modeling, **basic agent hygiene should be free and native**. SecureClaw ensures that your OpenClaw instance has a baseline defense layer out-of-the-box, acting as the first line of defense before any external APIs are even called.

---

Built by [Failsafe Security Inc.](https://getfailsafe.com)
