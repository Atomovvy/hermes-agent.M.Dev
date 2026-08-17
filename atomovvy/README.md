# Atomovvy Hermes overlay

Status: `FOUNDATION / THIN FORK / NO CORE AUTHORITY`

This directory contains Atomovvy-specific knowledge, provenance and Context Pack contracts layered on top of the upstream Hermes Agent fork.

## Upstream boundary

```text
UPSTREAM=NousResearch/hermes-agent
ATOMOVVY_FORK=Atomovvy/hermes-agent.M.Dev
PINNED_FOUNDATION_BASE=56526bc0d36522ab7a87ee0056f70e3847d2f0e6
UPSTREAM_LICENSE=MIT
UPSTREAM_CORE_REWRITE=NO
```

The upstream project remains the engine and user-facing mechanics. Atomovvy-specific work should remain at the edge whenever possible so upstream updates can continue to flow with minimal merge friction.

This follows the repository's own development guidance: keep the core narrow and put specialized capability at the edges.

## Atomovvy role

In Atomovvy Constellation, Hermes is a knowledge/context layer:

```text
knowledge
indexing
retrieval
context assembly
provenance
shared memory
```

Hermes is not:

```text
named Constellation agent
organizational authority
policy source
repository write permission source
implicit execution authorization
```

Mandatory invariant:

```text
HERMES_REMEMBERS_X != X_IS_AUTHORIZED
```

## First overlay contracts

```text
atomovvy/schemas/provenance.schema.json
atomovvy/schemas/context-pack.schema.json
atomovvy/examples/context-pack.example.json
atomovvy/POLICY_BOUNDARY.md
atomovvy/UPSTREAM_SYNC.md
```

These contracts are deliberately storage/transport neutral. They can be consumed later by a Hermes skill, service-gated tool, standalone adapter or external indexing process without adding a permanent core model tool merely to represent Atomovvy metadata.

## Provenance-first model

Every knowledge item should point back to a source rather than pretending a cached summary is canonical.

Examples of canonical source types:

```text
repository_file
commit
pull_request
issue
project_hub
approved_decision
runtime_evidence
research_source
```

A provenance record identifies what was observed, where it came from, which revision was observed and whether the source is canonical for the claim.

## Context Packs

A Context Pack is a bounded context assembly for one agent/task.

It contains:

```text
purpose
agent_id
generated_at
token_budget
freshness policy
items with provenance
authority classification
```

A Context Pack is not a prompt-authority escalation mechanism. Its items remain subject to current central/local policy and must be refreshed when their freshness contract requires it.

## No automatic execution

This foundation does not wire Hermes memory to GitHub writes, Codex, Local-Execution-Bridge, Agent Forum triggers or repository settings.

```text
HERMES_CONTEXT_TO_EXECUTION_AUTOMATION=NO
HERMES_AUTHORITY=NO
HERMES_POLICY_OVERRIDE=NO
```

Any future executable adapter requires separate capability, security and authority review.
