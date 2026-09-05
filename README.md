# Ak

Audit findings and strategy artifacts for the **Akolades** social + gaming-integration platform.

## Contents

| File | What it is |
|---|---|
| `BUG_MAP.md` | Full bug map from the authenticated click-through audit (all routes, Settings, Connections, Feed, Communities) |
| `bug-map.csv` | Machine-readable 11-bug map incl. the deep click-through findings (OAuth client_id failure, absent PSN/Xbox/Nintendo integrations, 401 auth flapping) |
| `bug3_connections_broken.png` | Screenshot evidence: every Connect button fails at Google OAuth (missing client_id) |
| `PHASED_DELIVERY.md` | Phase 0–4 delivery roadmap (stability → core loop → differentiation → scale) with implementation plans and reasoning |
| `GAMING_GAP_ANALYSIS.md` | Gap analysis vs Discord/Steam/Xbox/PSN/Riot/Twitch (the honest benchmark set), scored pillars + priority order |

## TL;DR

- 🔴 **BUG-003** — every account "Connect" button fails at OAuth (missing `client_id`). The gaming-integration core is non-functional; fix before anything else.
- 🟠 BUG-001 community 404 · BUG-002 suggestions 500 · BUG-004 Messaging placeholder
- 🟡 BUG-006 no PSN/Xbox/Nintendo connectors despite positioning
- Strategy: don't out-Facebook Facebook — win on **federated AI-native social + privacy-first moderation**, prove the loop with one platform (Steam), then broaden.
