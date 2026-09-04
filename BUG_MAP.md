# Akolades — Bug Map

> Comprehensive audit of the authenticated Akolades web app (social + gaming-integration platform).
> Scope: all primary routes, Settings area, account connections, community, and feed flows.
> Auth: `mike@akolades.com`. Findings captured via headless-browser click-through and API probing.

**Status legend:** 🔴 Critical · 🟠 High · 🟡 Medium · 🔵 Low · ⚪ Info

---

## Summary

| Severity | Count | Notes |
|----------|-------|-------|
| 🔴 Critical | 1 | Entire gaming/linked-account integration broken (OAuth) |
| 🟠 High | 3 | Community 404, Suggestions 500, Messaging placeholder |
| 🟡 Medium | 4 | Missing PSN/Xbox/Nintendo, Bookmarks placeholder, dead Linked-Accounts link, intermittent 401s |
| 🔵 Low | 2 | Inert post composer, CSP violation |
| ⚪ Info | 1 | Inert Upgrade-to-Premium |

**Most damaging finding (BUG-003):** the platform's core premise — connecting gaming accounts (Steam, Riot, Battle.net, Discord, Google) — fails at the OAuth step on every single "Connect" button.

---

## Critical

### BUG-003 — All "Connect" buttons broken (OAuth missing `client_id`)
- **Area:** Connections / Gaming integration
- **URL:** `https://www.akolades.com/settings/connections`
- **Severity:** 🔴 Critical
- **Description:** Every "Connect" button (Google, Battle.net, Riot Games, Discord, Steam) redirects to Google's OAuth error page:
  `Access blocked: Authorization Error — Missing required parameter: client_id`.
- **Impact:** The differentiating feature (one verified gaming identity across platforms) is completely non-functional.
- **Repro:** Log in → Settings → Connections → click any "Connect" button.
- **Status:** Confirmed

---

## High

### BUG-001 — Community not found on its own route
- **Area:** Communities
- **URL:** `https://www.akolades.com/communities/mikingdom`
- **Severity:** 🟠 High
- **Description:** Community `MiKingdom` (handle `mikingdom`) is returned by `CommunityService/ListUserCommunities`, but navigating to `/communities/mikingdom` renders *"Community not found. The community /mikingdom does not exist or may have been removed."*
- **Status:** Confirmed

### BUG-002 — Social suggestions API returns 500
- **Area:** Network / Discovery
- **URL:** `https://www.akolades.com/v1/social/suggestions?limit=20`
- **Severity:** 🟠 High
- **Description:** `GET /v1/social/suggestions?limit=20` → HTTP 500 `{"error":"internal error"}`. Fires on the Network page (Suggestions and Following tabs). UI silently falls back to *"Follow more people to unlock suggestions."*
- **Status:** Confirmed

### BUG-004 — Messaging not implemented
- **Area:** Platform / Primary nav
- **URL:** `https://www.akolades.com/messaging`
- **Severity:** 🟠 High
- **Description:** Primary nav "Messaging" renders placeholder *"Messaging is coming soon. Direct messages will be available…"* — a core social feature is unimplemented.
- **Status:** Confirmed

---

## Medium

### BUG-006 — PlayStation / Xbox / Nintendo integrations absent
- **Area:** Gaming integration
- **URL:** `https://www.akolades.com/settings/connections`
- **Severity:** 🟡 Medium
- **Description:** The platform is positioned to integrate PSN, Xbox Live, Nintendo, and Riot, but the Connections page only offers **Google, Battle.net, Riot Games, Discord, Steam**. No PlayStation Network, Xbox Live, or Nintendo options exist.
- **Status:** Confirmed

### BUG-005 — Bookmarks not implemented
- **Area:** Platform / Primary nav
- **URL:** `https://www.akolades.com/bookmarks`
- **Severity:** 🟡 Medium
- **Description:** Primary nav "Bookmarks" renders *"Coming in Phase 16"* — placeholder, feature incomplete.
- **Status:** Confirmed

### BUG-007 — Linked Accounts tab empty with dead link
- **Area:** Settings / Profile
- **URL:** `https://www.akolades.com/settings/linked-accounts`
- **Severity:** 🟡 Medium
- **Description:** Profile "Linked Accounts" tab shows *"No linked accounts — Connect accounts from your settings,"* but `/settings/linked-accounts` (and `/settings/accounts`) return **404**. The real page is `/settings/connections` — the link is broken/misleading.
- **Status:** Confirmed

### BUG-008 — Intermittent 401 authentication errors
- **Area:** Auth / Session
- **URL:** `https://www.akolades.com/akolades.identity.v1.IdentityService/GetCurrentUser`
- **Severity:** 🟡 Medium
- **Description:** `GetCurrentUser` and `/v1/users/me` intermittently return HTTP 401 *"authentication required"* even while logged in (observed during Settings navigation). Likely a token-expiry / silent-refresh bug.
- **Status:** Confirmed

---

## Low

### BUG-009 — Post composer has no visible editor
- **Area:** Feed
- **URL:** `https://www.akolades.com/feed`
- **Severity:** 🔵 Low
- **Description:** "Post / Photo / Video / Event" controls are present, but no textarea / contenteditable / textbox editor is rendered — the composer appears inert.
- **Status:** Confirmed

### BUG-010 — CSP violation loading Cloudflare beacon
- **Area:** All pages / Console
- **URL:** `https://static.cloudflareinsights.com/beacon.min.js`
- **Severity:** 🔵 Low
- **Description:** Console error on every page: *"Loading the script … violates the Content Security Policy."*
- **Status:** Confirmed

---

## Info

### BUG-011 — Upgrade to Premium appears inert
- **Area:** Billing
- **URL:** `https://www.akolades.com/settings/billing`
- **Severity:** ⚪ Info
- **Description:** "Upgrade to Premium" button does not navigate or open a checkout/pricing modal — stays on `/settings/billing`.
- **Status:** Unverified

---

## What's healthy

- **Settings area** is well-built: Account, AI, Nyx, Privacy, Billing, Sessions, Connections, Data — including data export, account deletion (30-day grace), privacy toggles, session management/revoke, and Nyx memory controls.
- **Feed interactions** work: Like, Comment, Repost, Bookmark, Post options.
- **Profile tabs** (Posts, Showcase, Communities, Linked Accounts) and the **Community create-modal** open correctly.

---

## Suggested priority

1. **BUG-003** — fix OAuth `client_id` (existential: unblocks all account/gaming connections)
2. **BUG-001 / BUG-002** — fix community routing + discovery 500 (platform can't grow with broken access/discovery)
3. **BUG-004 / BUG-005** — ship or gate Messaging + Bookmarks (core social features)
4. **BUG-006** — add PSN / Xbox / Nintendo connectors to match positioning
5. **BUG-008** — fix token refresh (affects all authenticated sessions)
6. Remaining: **BUG-007, BUG-009, BUG-010, BUG-011**

---

*Generated by agentic audit — headless-browser click-through + API probing. Screenshots available on request.*
