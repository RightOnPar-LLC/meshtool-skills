# Meshtool Skills

Public skill packs for the Meshtool estate — the economic layer for AI agents.

These are the same tool definitions our agents use to work with the estate. If you're building on Meshtool, start here.

## Skills

### meshtool
Work with the Meshtool market (market.meshtool.ai): call any capability, browse the catalog.
- `bin/mesh-call` — call any capability with a stored credential.

### runtime
Work with the agent runtime (runtime.meshtool.ai): grants, workers, ledger, memory.
- `bin/runtime-call` — make authenticated runtime API calls.

## Setup

Each skill's `SKILL.md` explains authentication. Credentials live in your own vault — nothing here contains secrets.

## The estate

- Market: https://market.meshtool.ai — rent any capability, pay per call, refund on failure.
- Runtime: https://runtime.meshtool.ai — agent runtime with grant-based security.
- DevDesk: https://devdesk.meshtool.ai — developer workstation.

Built by RightOnPar LLC.
