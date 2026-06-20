# agentpipeline

A reusable **multi-agent development workflow** for software projects — a small set of
documents that define roles, ticket flow, and anti-drift rules for running OpenAI
supervisors alongside Claude-based VS Code implementation agents.

The goal is to stop process drift, cut repeated explanation, and make one working
operating model portable across projects.

## What's Here

| File | Purpose |
|------|---------|
| [AGENTS.md](AGENTS.md) | Canonical short instruction set every agent reads first — roles, default pipeline, ticket and handoff rules, anti-drift protocol. |
| [agent-orchestration-model.md](agent-orchestration-model.md) | Full workflow detail — role map, success/failure modes, pipeline variations, drift definition, operator authority. |
| [TICKET_TEMPLATE.md](TICKET_TEMPLATE.md) | The ticket format used for all substantive work units. |

## The Model in Brief

**Two layers:**
- **OpenAI supervisors** — strategy, ticket framing, architecture, and drift detection.
- **Claude VS Code coders** — heavy implementation, review, diagnostics, and security audit.

**Roles:**
- `Supervisor 1` — master ticket owner, strategic planner, workload allocator
- `Supervisor 2` — architecture owner, drift monitor, quality gate
- `VS Code Coder 1` — primary implementation (full write access)
- `VS Code Coder 2` — review and correction
- `VS Code Diagnostics` — read-only investigation and evidence gathering
- `VS Code Security Auditor` — optional targeted security review
- `Operator` — final human authority on ambiguity, repeated drift, or strategy

**Default pipeline:**

```
Supervisor 2  →  Supervisor 1  →  Coder 1  →  Coder 2  →  Diagnostics  →  Supervisor 2
(constraints)    (ticket)         (build)     (review)    (if needed)     (drift check)
```

Shorter paths are allowed for small or low-risk changes. Add roles when work spans
architecture and implementation, when an agent has already looped, or when touching
pipelines, auth, secrets, or data handling.

## How to Use

1. Drop these files into a project (or reference this repo as the shared standard).
2. Every agent reads [AGENTS.md](AGENTS.md) before working.
3. Open a ticket from [TICKET_TEMPLATE.md](TICKET_TEMPLATE.md) for any substantive task.
4. Follow the default pipeline; escalate per the anti-drift protocol when an agent
   starts patching symptoms instead of the cause.

## Anti-Drift Protocol

When a loop is detected: stop speculative edits → capture what was attempted →
gather read-only diagnostics → escalate to `Supervisor 2` to reframe →
return to `Supervisor 1` for a cleaner ticket → escalate to `Operator` if still ambiguous.

---

> The docs reference a `v2` personal-archive RAG as the originating project, but the
> orchestration model itself is project-agnostic and meant to be reused.
