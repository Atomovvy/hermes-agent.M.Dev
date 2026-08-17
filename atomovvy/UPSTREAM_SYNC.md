# Atomovvy Hermes upstream sync strategy

## Goal

Keep `Atomovvy/hermes-agent.M.Dev` close to `NousResearch/hermes-agent` while concentrating Atomovvy-specific knowledge contracts under `atomovvy/`.

## Default rule

```text
UPSTREAM_MECHANICS=REUSE
ATOMOVVY_OVERLAY=ISOLATED
CORE_PATCH=EXCEPTION
```

Do not modify upstream core merely to carry Atomovvy metadata, governance or Context Pack semantics when an overlay/adapter can do the job.

## Sync review

Before integrating a future upstream update:

1. identify the exact upstream revision,
2. review upstream license and relevant changed files,
3. verify `atomovvy/` remains isolated from changed upstream mechanics,
4. resolve only real conflicts,
5. revalidate Atomovvy schemas/examples,
6. separately validate any actual core patch if one exists.

## Escalation rule

A core modification is justified only when a concrete consumer cannot be implemented safely as an edge capability such as:

```text
existing extension point
CLI command + skill
service-gated tool
standalone adapter/plugin
MCP server
```

If a core change becomes necessary, document why each lower-footprint option is insufficient and validate against upstream caching/session invariants.

## No upstream identity rewrite

Do not rewrite upstream copyright, license, README authorship or project identity to make the fork appear to be original Atomovvy code.

The Atomovvy overlay documents Atomovvy-specific additions while preserving upstream provenance.
