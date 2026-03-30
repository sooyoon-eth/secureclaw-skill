# SecureClaw: Best Practices for Agent Security

Implementing the `PROMPTS.md` is the first step. To ensure your OpenClaw instance remains truly secure, follow these architectural best practices.

## 1. Principle of Least Privilege

Your agent should only have access to the tools and permissions it absolutely needs to function.

- **Terminal Access:** If your agent doesn't need to run terminal commands, disable the terminal tool entirely. If it does, run it in an isolated container or restricted environment, not on your host machine.
- **File System:** Restrict file read/write access to a specific workspace directory. Never give the agent access to the root filesystem (`/`) or user home directory (`~`).

## 2. Environment Variable Segregation

- Never expose critical infrastructure API keys (AWS, production databases) to an agent unless it is explicitly designed for DevOps operations.
- Store keys in a secure `.env` file and ensure the agent's prompts forbid reading `.env` files or using commands like `printenv`.

## 3. Human-in-the-Loop (HITL) for High-Risk Actions

Native prompts can only go so far against a determined attacker. For high-risk operations, implement a strict HITL requirement:

- **Financial Transactions:** Any transfer of funds must require human approval.
- **Destructive Operations:** Commands like `rm -rf`, dropping database tables, or modifying cloud infrastructure should trigger an approval workflow.

## 4. Monitor Your Agent's Logs

Agents are targets for manipulation. Regularly review your agent's conversation logs and terminal outputs for anomalies. Look for patterns such as:

- Encoded strings (Base64) in user input
- Repeated attempts to access `.env` or configuration files
- Unexpected outbound network connections

## 5. Defense-in-Depth

SecureClaw provides native, free, baseline security. However, as your agent handles more value or sensitive data, consider layering external security services (like ARGUS or other intelligence providers) to catch sophisticated, constantly evolving threats that a static prompt cannot detect.
