---
name: "meshtool"
description: "Use Meshtool when the user asks for Meshtool or this provider's API."
---

# Meshtool

## Purpose
Use Meshtool with the user-connected `custom.meshtool` credential.

## Tooling
Add service-specific CLIs under `~/workspace/skills/meshtool/bin/`.

- `mesh-call <slug> '<json-input>'` — call a MeshMarket capability; Bearer auth is
  attached automatically via the stored `custom.meshtool` credential. Browser-like
  User-Agent required (Cloudflare 1010 blocks default urllib UA).
- Public (no-auth) endpoints: `GET /api/capabilities` (48 listed, with price in
  MESH), `GET /api/health`, `GET /api/stats`. Live no-signup demos:
  `https://market.meshtool.ai/call?try=<slug>` (funded demo node).

Python CLIs must import `/opt/hatch/skills/skill-creator/bin/dynamic_credentials.py` and call `add_surrogate_to_request(...)`, `url_with_surrogate_query_param(...)`, or `url_with_surrogate_path_segment(...)` before authenticated requests, matching where the provider reads the key. If they use `urllib`, read JSON responses with `read_json_response(resp)` from the same helper instead of calling `resp.read()` directly. They must send only `hsurr:*` values, and only to the hosts below.

## Auth
The credential is already stored; nothing here collects one. Never ask the user to paste a raw key in chat, set a secret environment variable, pass a secret flag, or write an auth file.

A 401 or 403 is a question about the request before it is a question about the key. Check that the credential was attached at all: a request built without the helpers named under Tooling carries nothing, and that looks exactly like a wrong or under-scoped token. Only once a request that did carry the credential is still rejected, call `credentials.request_api_access` with `reconnect` to replace it. The connector is stored as `custom.meshtool`.

## Operating Rules
1. Use this skill when the user asks for Meshtool or this provider's API.
2. Restrict authenticated requests to: market.meshtool.ai.
3. Do not print, log, or persist raw credentials.
4. If auth is missing or rejected, follow the Auth section rather than asking for a key.
