# agentic-ai-governance-framework

A production-grade Zero Trust security framework, dynamic IAM architecture, and Policy-Based Access Control (PBAC) engine designed to secure task-oriented, autonomous AI agents against Indirect Prompt Injection, Excessive Agency, and Unauthorized Tool Execution.

---

## Executive Summary

As enterprise organizations deploy autonomous AI agents across core operational domains (Customer Support, Finance, HR, and Infrastructure Ops), traditional security perimeters and static Role-Based Access Control (RBAC) fail to contain non-deterministic model behavior. 

This repository provides an end-to-end Governance, Risk, and Compliance (GRC) and SecOps architecture built for **Apex Cloud Solutions**. It addresses the systemic security threats posed by unrestricted agentic tool execution through a decoupled **Policy Decision Point (PDP)**, ephemeral **Just-In-Time (JIT)** credential brokering, and deterministic **Human-In-The-Loop (HITL)** interception gates.

---

## Core System Architecture

[ External Untrusted Payload ] (Support Tickets, Invoices, Webhooks)
│
▼
┌──────────────────────────────┐        ┌───────────────────────────────────┐
│  Autonomous AI Agent Engine  │ ─────> │ Centralized OPA / Policy Engine   │
└──────────────────────────────┘        └─────────────────┬─────────────────┘
│ (Evaluates ABAC & Context)
▼
┌───────────────────────────────────┐
│    Dynamic Authorization Gate     │
└─────────────────┬─────────────────┘
│
┌────────────────────────────────────────────┼────────────────────────────────────────────┐
▼                                            ▼                                            ▼
[ Low-Risk Executions ]                      [ High-Risk Threshold ]                      [ Security Telemetry ]
• Microsegmented RBAC                        • JIT OAuth Token Issued (TTL ≤ 15m)          • Real-Time SIEM Audit Stream
• Read-Only API Limits                       • Mandatory HITL MFA Gatekeeper              • Dual-Claim (sub/act) Tracing

---

## Architecture Principles & Core Safeguards

** Zero Trust Non-Human Identity (NHI):** Eliminates static API keys and shared service accounts. AI agents operate under isolated workload identities using OAuth 2.0 Client Credentials Grant and Token Exchange ([RFC 8693](https://datatracker.ietf.org/doc/html/rfc8693)).
** Dual-Claim Auditability:** Every downstream API request contains dual-claim JWT tracking:
  * `sub` *(Subject)*: Tracks the end-user initiating or benefiting from the request.
  * `act` *(Actor)*: Tracks the specific agent workload executing the transaction for non-repudiation.
** Contextual Attribute-Based Access Control (ABAC):** Evaluates agent requests at runtime against monetary limits (e.g., auto-approve refunds $\le \$100$), rate limits, environmental tiers, and verified ticket IDs.
** Ephemeral JIT Credential Brokering:** Restricts agent privileges to dynamic tokens with strict Time-To-Live expiration ($\le 15$ minutes).
** Human-In-The-Loop (HITL) Interception:** Enforces manual human authorization/MFA for high-impact state changes (e.g., Stripe payouts $> \$100$, database writes, IAM policy changes).

---

## Deliverables & Repository Structure

📁 AGENTIC-AI-SECURITY-FRAMEWORK/
│
├── 📜 README.md                                  # Master System Architecture & Index
│
├── 📁 01_GOVERNANCE_AND_THREAT_MODELING/
│   ├── 📄 Deliverable_01_Threat_Model.md         # 10 Agentic AI Security Risks (OWASP/STRIDE)
│   └── 📄 Deliverable_02_Agent_Inventory.md      # Business ownership, scope & SoD mapping
│
├── 📁 02_IDENTITY_AND_ACCESS_CONTROL/
│   ├── 📄 Deliverable_03_IAM_Architecture.md     # Non-Human Identity (NHI) & Token Exchange
│   ├── 📄 Deliverable_04_Permission_Matrix.md    # Fine-Grained ABAC Policy Matrix
│   └── 📄 Deliverable_05_JIT_Access_Spec.md      # Ephemeral token workflow & Break-Glass protocol
│
└── 📁 03_GOVERNANCE_POLICY_AND_REPORTS/
└── 📄 Deliverable_06_Enterprise_AI_Policy.md # Enterprise AI Agent Security Policy (NIST/ISO)

---

## Master Deliverable Directory

| Ref # | Deliverable File | Core Security Focus & Standards Alignment |
| :---: | :--- | :--- |
| ** 01 ** | `Deliverable_01_Threat_Model.md` | Threat modeling 10 agentic risks against **OWASP Top 10 for LLMs** and **STRIDE**. |
| ** 02 ** | `Deliverable_02_Agent_Inventory.md` | Establishing Separation of Duties (SoD) across SupportBot, LedgerBot, TalentBot, and OpsMonitor. |
| ** 03 ** | `Deliverable_03_IAM_Architecture.md` | Designing Non-Human Identities, RFC 8693 Token Exchange, and dual-claim tracing (`sub`/`act`). |
| ** 04 ** | `Deliverable_04_Permission_Matrix.md` | Enforcing default-deny runtime ABAC rules and hard monetary execution boundaries. |
| ** 05 ** | `Deliverable_05_JIT_Access_Spec.md` | Defining short-lived credential workflows, JSON policy payloads, and emergency break-glass steps. |
| ** 06 ** | `Deliverable_06_Enterprise_AI_Policy.md` | Formal organizational AI Governance Policy aligned with **NIST AI RMF** and **ISO/IEC 42001**. |

---

## Security Audit Verification Summary

- [x] ** Zero Static Wildcards:** No wildcard (`*`) permissions granted across any agent scope.
- [x] ** Credential Protection:** Zero hardcoded API keys or persistent environment secrets.
- [x] ** Blast Radius Containment:** Unsanctioned tool invocation and administrative actions strictly isolated.
- [x] ** Separation of Duties:** Financial transactions and infrastructure changes isolated from customer-facing agents.

---

## License & Attribution

Architected as an open-source cybersecurity portfolio blueprint by **Oriade Adewale Emmanuel**. Released under the [MIT License](LICENSE).
