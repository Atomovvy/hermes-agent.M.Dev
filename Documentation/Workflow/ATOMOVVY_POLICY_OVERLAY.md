# Atomovvy policy overlay for hermes-agent.M.Dev

This file is an Atomovvy-local operating overlay for the external-copy repository `Atomovvy/hermes-agent.M.Dev`.

## Upstream boundary

The upstream Hermes Agent project is built by Nous Research and already provides its own root `AGENTS.md`. That upstream instruction file remains intact and continues to govern Hermes product architecture, contribution expectations and implementation conventions.

```text
REPOSITORY_ROLE=EXTERNAL_COPY
UPSTREAM_PROJECT=NousResearch/hermes-agent
UPSTREAM_AGENTS_PRESERVED=YES
LOCAL_ATOMOVVY_OVERLAY!=UPSTREAM_PROJECT_POLICY
```

The current repository license is MIT. Preserve upstream copyright and license notices.

## Atomovvy authority boundary

For Atomovvy-directed repository work, current `Atomovvy/Atomovvy` central policy governs repository authority, Git safety, coordination, validation and handoff. The upstream `AGENTS.md` cannot grant Atomovvy cross-repository write authority, merge authority, local execution authority or permission to weaken central safety rules.

Before an Atomovvy-specific repository mutation, read current central `MULTI_AGENT_LOCK_POLICY.md` and `P2C_SIMPLE_LOCK_V2_RUNBOOK.md` together with `Documentation/Workflow/REPO_POLICY_MANIFEST.md` and the upstream root `AGENTS.md`.

## External-agent risk boundary

Hermes exposes broad agent capabilities including terminal backends, plugins, skills, MCP, messaging gateways, scheduled automation, memory and subagents. This rollout changes none of those capabilities and grants no authority to execute Hermes, connect providers, use credentials, contact messaging platforms, run cron jobs, invoke terminals, install plugins/skills or access user data.

```text
REPOSITORY_WRITE_COORDINATION!=AGENT_EXECUTION_AUTHORITY
REPOSITORY_WRITE_COORDINATION!=NETWORK_AUTHORITY
REPOSITORY_WRITE_COORDINATION!=CREDENTIAL_AUTHORITY
REPOSITORY_WRITE_COORDINATION!=SCHEDULED_AUTOMATION_AUTHORITY
```

## Repository writer coordination

For ordinary hosted Atomovvy GitHub mutations in this repository, use P2-C Simple Lock v2:

```text
P2C_SIMPLE_LOCK_V2_STATUS=ACTIVE
COORDINATION_MODE=P2C_SIMPLE_LOCK_V2
LOCK_REF=coordination/write-lock-v2
LOCK_FILE=LOCK.json
P2C_LEGACY_STRONG_STATUS=FROZEN_REFERENCE
LEGACY_STRONG_DEFAULT_FOR_ORDINARY_WRITES=NO
```

Freshly fetch and validate the live lock, acquire it by exact file-SHA compare-and-swap, and verify exact ownership before the first ordinary mutation. Read-only work does not require the lock. Coordination failure fails closed without Legacy Strong fallback.

The lock coordinates conforming Atomovvy writers only. It does not replace Git/target freshness, upstream provenance and licensing review, upstream development constraints, security review, validation or merge authority.

## Git and upstream synchronization

Atomovvy-specific tracked changes use a dedicated branch and Draft PR. Upstream synchronization, rebases, force pushes, history rewriting, product releases and merges require separate bounded review and authority.
