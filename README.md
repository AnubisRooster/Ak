# Ak

Bug map and audit findings for the **Akolades** social + gaming-integration platform.

## Contents

- `BUG_MAP.md` — Full bug map from an authenticated click-through audit (all routes, Settings, Connections, Feed, Communities).

## Summary

The platform's core premise is "one verified gaming identity across PlayStation, Steam, Xbox, Nintendo, and Riot." The audit found:

- 🔴 **BUG-003** — Every account "Connect" button fails at OAuth (missing `client_id`). The entire gaming-integration core is non-functional.
- 🟠 **BUG-001** — Communities 404 on their own route.
- 🟠 **BUG-002** — Social suggestions API returns HTTP 500.
- 🟠 **BUG-004** — Messaging is a placeholder.
- 🟡 **BUG-006** — PlayStation / Xbox / Nintendo integrations are absent (only Google, Battle.net, Riot, Discord, Steam are offered).

See `BUG_MAP.md` for the full detail.
