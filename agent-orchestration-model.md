# Agent Orchestration Model

## Why This Exists

This repository is developed using a multi-agent workflow across OpenAI supervisors and Claude-based VS Code implementation agents.

The purpose of this document is to stop process drift, reduce repeated explanation, and make the working model reusable across projects.

## Operating Reality

The operator commonly runs multiple projects in parallel.

Typical structure per project:

- up to 2 supervisors
- up to 3 implementation and support agents in VS Code
- optional diagnostics and security agents

OpenAI is used as the supervisory layer because it is trusted for strategy, ticket framing, and drift detection.

Claude in VS Code is used as the heavy implementation layer because it supports native IDE workflows and lower-cost high-volume coding.

## Role Map

### Supervisor 1

Responsibilities:

- master ticket owner
- strategic planner
- workload allocator
- primary project direction keeper

Success condition:

- tickets remain clear, bounded, and outcome-focused

Failure mode:

- strategy drifts into implementation detail
- ticket framing becomes vague or overloaded

### Supervisor 2

Responsibilities:

- architecture owner
- drift monitor
- quality gate before and after implementation
- correction point when the pipeline goes off track

Success condition:

- implementation stays aligned to architecture and product direction

Failure mode:

- acts too late after drift has already become expensive

### VS Code Coder 1

Responsibilities:

- raw implementation
- file changes
- direct code execution
- first-pass validation

Success condition:

- moves tickets forward with concrete code changes

Failure mode:

- loops on local fixes
- overfits to the last prompt
- makes code look busy while missing the real issue

### VS Code Coder 2

Responsibilities:

- code review
- correction review
- identifying logic regressions or weak fixes

Success condition:

- catches missed defects and weak implementations

Failure mode:

- duplicates coder work instead of reviewing it

### VS Code Diagnostics

Responsibilities:

- read-only investigation
- evidence gathering
- narrowing unknowns before rework

Success condition:

- provides facts instead of speculation

Failure mode:

- starts proposing architecture without enough context

### VS Code Security Auditor

Responsibilities:

- optional targeted security review
- secrets, access, data exposure, unsafe dependencies, risky flows

Success condition:

- catches issues before they become operational risk

## Standard Pipeline

Default flow:

1. `Supervisor 2` sets constraints, architecture notes, or drift warnings
2. `Supervisor 1` writes the working ticket
3. `VS Code Coder 1` implements
4. `VS Code Coder 2` reviews
5. `VS Code Diagnostics` investigates if needed
6. work returns to `Supervisor 2` for architecture and drift check

This is the default, not a rigid rule.

Allowed shorter paths:

- `Supervisor 1 -> Coder 1` for small isolated fixes
- `Supervisor 2 -> Diagnostics -> Supervisor 1` when the problem is unclear
- `Supervisor 1 -> Security Auditor` when the task is security sensitive

## When To Add Or Remove Roles

Use fewer roles when:

- the change is tiny
- the architecture is already stable
- the risk of drift is low

Use more roles when:

- the task spans architecture and implementation
- the agent has already looped once
- the repo is dirty or confusing
- the system is changing pipelines, retrieval, auth, secrets, or data handling

## Drift Definition

Drift means the implementation no longer matches the real goal.

Common drift patterns:

- the agent keeps fixing symptoms instead of the cause
- the task gets trapped in repeated prompt edits
- the implementation overfits to one corpus or one test case
- the agent keeps changing code without improving validation results
- the agent starts restating progress instead of producing it

## Anti-Loop Protocol

When a loop is detected:

1. stop new speculative edits
2. capture what was attempted
3. request read-only diagnostics if facts are missing
4. escalate to `Supervisor 2` for reframing
5. return to `Supervisor 1` for a cleaner ticket
6. escalate to `Operator` if the problem is still ambiguous or strategic

## Operator Authority

Only the operator can make final decisions when:

- multiple plausible paths remain
- the agent stack is stuck
- repeated loops continue
- the product objective itself needs reframing

Agents should not pretend certainty when operator judgment is required.

## Ticket Architecture

Every meaningful work unit should be ticketed.

Required ticket characteristics:

- one owner
- one clear next handoff target
- explicit scope boundary
- explicit validation expectation
- optional operator review section
- completion handoff that explains outcome, not just activity

See:

- [tickets/TICKET_TEMPLATE.md](C:/Users/z/Desktop/code/legal-ai/tickets/TICKET_TEMPLATE.md)

## Handoff Pattern

Each completed task should include:

- `Handoff To`
- `Status`
- `What Changed`
- `Validation Run`
- `Risks / Drift Notes`
- `Next Recommended Ticket`
- `Operator Review` if needed

## Quality Gate Principles

Supervisors should favor:

- reproducibility
- architecture clarity
- measurable outcomes
- evidence-backed diagnosis
- concise user-facing summaries

Do not favor:

- prompt-only correction cycles
- vague “should work now” claims
- repeated edits without better validation
- retaining broken structure just because it already exists

## Project-Specific Fit For This Repo

For this repo, the orchestration model should support:

- `v2` as a personal archive RAG
- multi-domain corpora
- metadata-aware retrieval
- grounded summary and expansion modes
- accessibility-first output for low reading load

## Long-Term Meta-Project Potential

This operating model can itself become a product:

- one IDE or workspace
- many agent tabs
- multiple model providers
- role-based routing
- shared ticket memory
- supervisor-enforced anti-drift workflow

That concept is valid and worth preserving for future work.
