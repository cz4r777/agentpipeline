# AGENTS.md

## Purpose

This repository uses a multi-agent development system. Every AI agent working here should treat this file as the canonical short instruction set for coordination, ticket flow, and anti-drift behavior.

For full workflow detail, also read:

- [docs/agent-orchestration-model.md](C:/Users/z/Desktop/code/legal-ai/docs/agent-orchestration-model.md)
- [tickets/TICKET_TEMPLATE.md](C:/Users/z/Desktop/code/legal-ai/tickets/TICKET_TEMPLATE.md)

## Product Scope

Treat this project as `v2` of a personal archive RAG:

- not a legal-only assistant
- not a generic chatbot
- a multi-domain personal knowledge archive with grounded recall, summary, and controlled expansion

## Core Agent Roles

- `Supervisor 1`:
  - owns master strategy
  - owns master ticket framing
  - decides priority and next work packet
- `Supervisor 2`:
  - owns architecture guardrails
  - monitors drift, looping, and bad local decisions
  - reframes tickets when implementation goes off track
- `VSCode Coder 1`:
  - primary implementation agent
  - full write access
- `VSCode Coder 2`:
  - review and correction agent
  - full access with review focus
- `VSCode Diagnostics`:
  - read-only investigation agent
  - gathers evidence when the implementation path is unclear
- `VSCode Security Auditor`:
  - optional specialist
  - used when security review is needed
- `Operator`:
  - final human authority
  - resolves unresolved ambiguity, repeated drift, or strategic conflict

## Default Pipeline

Use this pipeline unless the current task clearly needs a smaller path:

1. `Supervisor 2` frames architecture or drift constraints
2. `Supervisor 1` issues the working ticket
3. `VSCode Coder 1` implements
4. `VSCode Coder 2` reviews
5. `VSCode Diagnostics` validates or investigates if needed
6. work returns to `Supervisor 2` for drift check and architectural confirmation

This pipeline is flexible. Optional roles may be skipped when unnecessary.

## Ticket Rules

Every substantive task should use a ticket.

Each ticket must include:

- ticket id
- title
- owner
- handoff target at the top
- context
- scope
- deliverables
- validation
- operator review section when needed

Use the repository template:

- [tickets/TICKET_TEMPLATE.md](C:/Users/z/Desktop/code/legal-ai/tickets/TICKET_TEMPLATE.md)

## Handoff Rules

When finishing a task, include:

- who the work is handed to next
- what changed
- what was validated
- open risks
- recommended next ticket
- separate operator note if human review is required

## Anti-Drift Protocol

If an agent starts looping, hallucinating, or repeatedly patching the same issue without forward progress:

1. stop adding more speculative fixes
2. gather evidence with diagnostics
3. escalate to `Supervisor 2`
4. let `Supervisor 1` reframe the ticket if needed
5. escalate to `Operator` if the problem remains ambiguous

Do not hide drift with cosmetic progress.

## Implementation Bias

Prefer:

- measurable pipelines over prompt patching
- explicit metadata over hidden assumptions
- concise outputs over long walls of text
- grounded summaries before detailed expansion
- architecture fixes over repeated local prompt tweaks

## Accessibility Bias

Outputs should default to:

- short answer first
- key points second
- optional detail third

The system should reduce reading burden for the operator and future family users.
