# Akolades — Phased Delivery Roadmap

> Gaming-social platform positioning: one verified gaming identity across
> PlayStation, Steam, Xbox, Nintendo, and Riot, federated, privacy-first, with
> an AI companion (Nyx) that operates in your community.
> Ordering logic: **stability → core loop → differentiation → scale/monetization.**

---

## Phase 0 — Stabilize the foundation (Week 1–2)
**Goal:** the app works before it grows. Zero confirmed defects (see `bug-map.csv`).

**Scope:** BUG-003 (OAuth client_id — existential, blocks all account connections), BUG-001 (community route 404), BUG-002 (suggestions 500), BUG-004/005 (Messaging/Bookmarks: ship or gate).

**Plan:**
1. Reproduce each bug as a Playwright regression test (mirroring the audit scripts)
2. BUG-001: fix handle↔route resolution — the slug `mikingdom` must resolve via `ListUserCommunities`
3. BUG-002: server-side error handling on `SocialGraphService`; structured empty result, not `internal error`; honest client fallback
4. Messaging/Bookmarks: ship minimal versions or explicit "Phase N" screens (correct nav state)
5. Smoke tests: every primary route post-login asserts no 4xx/5xx, no "not found"/"coming soon"

**Reasoning:** everything depends on these; broken discovery and broken community access are fatal for a social product. Fastest credibility win.

---

## Phase 1 — Prove the core loop: ONE platform integration (Week 3–6)
**Goal:** end-to-end thesis proof: *one verified gaming identity → presence → activity → find friends.*

**Scope — Steam first:** OAuth linking, verified profile (playtime, library, currently-playing, achievements), activity feed ("X started playing Y"), presence sync, friend-matching (Steam friends → AkoladesID).

**Plan:**
1. Platform-account model + Steam OpenID/Web API OAuth; link against existing AkoladesID ("Linked Accounts" surface is the hook)
2. Ingestion pipeline → `GameActivity` + `PlatformIdentity` schema
3. Activity feed off ingested events (reuse Feed UI)
4. Presence service (poll/WebSocket) tied to connected platforms
5. Friend-graph reconciliation (federation flags already on)
6. Instrument everything for Phase 4 analytics

**Reasoning:** make-or-break proof. Validates the premise with one well-documented integration before stricter PSN/Xbox/Nintendo/Riot partner processes. **The linchpin — everything downstream assumes it works.**

---

## Phase 2 — Expand integrations + ship the social core (Week 7–12)
**Goal:** breadth + the features that make it *social*.

**Scope:** Xbox Live, PSN, Nintendo, Riot connectors; **ship Messaging** (1:1 + group + channels, low-latency presence); **ship Bookmarks**; community upgrades (game channels, clans, LFG, rosters); real search + working suggestions.

**Plan:** abstract a `PlatformConnector` interface from the Steam work; WebSocket messaging with persistence (the Discord-competitor surface — invest here); community `game` association + channel taxonomy + member roles; index profiles/communities/posts and replace the 500ing suggestions endpoint with real recommendations.

**Reasoning:** Phase 1 proved it; Phase 2 industrializes it. Messaging and communities are the engagement moat.

---

## Phase 3 — Differentiate: Nyx as product + privacy-first moderation GA (Week 13–18)
**Goal:** build what neither Discord nor Steam have.

**Scope:** Nyx productized (game-native skills: raid/event scheduling, LFG coordination, patch-notes summaries, stat lookups triggered by presence + community context; federation across Discord/Slack/Telegram as interop); moderation infrastructure to GA (operator-in-the-loop dashboards, review queues, policy engine, agentic MCP endpoints — packaged as a separate offering); privacy controls (per-platform sharing toggles, "show gaming identity, hide real identity").

**Plan:** define Nyx's skill-cards/triggers/permission model/memory controls; wire Nyx into community events + presence; productize moderation into a partner-facing SKU; public docs + onboarding.

**Reasoning:** the category wedge — a federated AI copilot plus privacy-first moderation is the defensible moat that makes out-scaling Facebook irrelevant. Sequenced after the core loop exists so it has a platform to attach to.

---

## Phase 4 — Scale & monetize (Week 19+)
**Goal:** growth, revenue, ecosystem.

**Scope:** subscription tiers, creator monetization, premium community features, event/tournament ticketing; analytics for community owners; public API + developer ecosystem (agentic MCP endpoints); mobile apps; growth loops (invites, cross-platform friend-import).

**Plan:** tier boundaries from Phase 3 usage data; admin analytics dashboards; developer portal; React Native/Flutter wrappers with push presence; import/onboarding-template flows.

**Reasoning:** monetization and ecosystem only make sense once engagement and differentiation exist. The AI + moderation offering adds a B2B revenue vector pure social networks lack.

---

## Cross-phase guardrails
- **Fix-then-feature:** no new phase starts with open P0/P1 defects (Phase 0 gates everything)
- **One-platform proof before breadth:** no PSN/Xbox until Steam validates the loop
- **Privacy-first by default:** "don't sell community data / operator-in-the-loop" is brand — a hard constraint in every integration
- **Measure activation, not vanity:** linked account + first activity; weekly active in communities; friend-join rate

## Critical dependency
Phase 1's Steam end-to-end loop. If it fails to produce a compelling cross-platform identity experience, re-scope the rest of the roadmap.
