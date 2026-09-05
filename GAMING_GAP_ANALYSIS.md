# Akolades — Gaming-Social Gap Analysis

> Benchmark recalibration: the rival set is **Discord, Steam Community, Xbox/PSN
> social, Riot, Twitch** — not Facebook/LinkedIn. The differentiating thesis:
> **"One verified gaming identity across every platform, federated, privacy-first,
> with an AI companion (Nyx) that operates in your community."**

Scores are current state vs. required-for-parity (0–10), grounded in the
authenticated app audit (see `bug-map.csv`).

## The gaps

| # | Pillar | Now | Need | The gap |
|---|--------|-----|------|---------|
| 1 | **Platform account integration** — the core premise | 1 | 9 | No live PSN/Steam/Xbox/Nintendo/Riot OAuth (only Akolades Keycloak); every Connect button fails at OAuth (BUG-003); Connections offers only Google/Battle.net/Riot/Discord/Steam — **no PSN/Xbox/Nintendo at all** (BUG-006) |
| 2 | **Gaming-native profile** | 2 | 9 | Generic bio + handle; no trophies/achievements, playtime, library, rank/tier, "currently playing", squad/party, platform presence |
| 3 | **Communities with gaming structure** | 4 | 8 | Communities exist but no clans/guilds, LFG, raid/event scheduling, voice, team rosters, game channels |
| 4 | **Messaging (real-time)** | 0 | 9 | Placeholder ("coming soon", BUG-004). Discord's moat is real-time voice/text + presence — existential for gaming-social |
| 5 | **Discovery & search** | 1 | 8 | Suggestions API 500s (BUG-002); community route 404s (BUG-001); no people/community search |
| 6 | **Presence & activity feed** | 1 | 8 | No online/in-game status, no game-activity feed, no status synced from connected platforms |
| 7 | **Cross-platform friend graph** | 0 | 9 | The killer feature — resolve one human across PSN+Steam+Xbox+Riot and unify their social graph. Federation is a foundation, not the same thing |
| 8 | **Events & tournaments** | 0 | 7 | No structured events/LFG scheduling product (Nyx reminders are manual) |
| 9 | **Monetization (gaming-native)** | 0 | 7 | Free tier only; no premium tied to features, creator/clip monetization, or event ticketing |
| 10 | **Moderation & safety** | **7** | 9 | **The genuine advantage**: moderation infrastructure, operator-in-the-loop, "don't sell community data", forseti_moderation enabled. Gaming needs this badly (toxicity, scams) — parents/communities are the buyers |
| 11 | **AI/assistive layer (Nyx)** | **6** | 8 | Novel: game character lookups, patch notes, event coordination, cross-platform federation. Neither Discord nor Steam has an integrated social-native AI companion |

## What the current product already has (foundations that align)

- Communities (matches the server/clan/guild model)
- AkoladesID + handles + "Linked Accounts" surface (the hook for platform linking)
- Federation inbound/outbound flags enabled (unusual and powerful for cross-platform identity)
- Nyx across Discord/Slack/Telegram
- Well-built Settings area (Account, AI, Nyx, Privacy, Billing, Sessions, Connections, Data — export, 30-day deletion, memory controls)

## Strategic read

Do **not** out-Facebook Facebook. The credible path is a differentiated niche on
the two genuine strengths:

1. **Moderation infrastructure** (operator-in-the-loop, privacy-first) — the trust wedge
2. **Federated + AI-native social** (Nyx across platforms, federation enabled) — the product wedge

## Priority order

1. **Fix the 4 confirmed launch-blocking bugs** (BUG-003 first — the integration core is dead on arrival)
2. **Ship ONE platform integration end-to-end** (Steam): link → verified profile → presence → feed → find friends
3. **Build presence + activity feed** off that integration
4. **Productize Nyx** around the gaming workflow (raid/event scheduling, LFG, patch notes, stats)
5. **Messaging** before broad launch

Nobody currently owns "one verified gaming identity, federated, with an AI
copilot." That combination is the wedge.
