# Ticket Template

Use this template for substantive multi-agent work.

```text
Ticket: LEGALAI-XXX
Title:
Priority:
Status:
Owner:
Handoff To:
Depends On:

Operator Review:
- required: yes/no
- question:

Context:

Objective:

Scope:
- in scope:
- out of scope:

Deliverables:
- deliverable 1
- deliverable 2

Architecture / Drift Guardrails:
- guardrail 1
- guardrail 2

Validation:
- command or check 1
- command or check 2

Completion Handoff:
- status:
- files changed:
- validation run:
- risks:
- next recommended ticket:
- note to operator:
```

## Minimal Rules

- `Handoff To` must appear near the top
- `Operator Review` can be omitted only when clearly unnecessary
- scope must be bounded
- completion handoff must say what happened, not just what was attempted

## Suggested Handoff Targets

- `Supervisor 1`
- `Supervisor 2`
- `VSCode Coder 1`
- `VSCode Coder 2`
- `VSCode Diagnostics`
- `VSCode Security Auditor`
- `Operator`
