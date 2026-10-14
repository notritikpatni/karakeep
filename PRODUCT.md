# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Ritik Patni — a single power user. Primary surface is the web app on desktop (most-used platform, the one the fork optimizes); the phone app and browser extension serve capture from away-from-desk situations. Occasional shared lists may exist, but multi-user features stay out of the way rather than being surgically removed.

## Product Purpose

A self-hosted "second brain" capture desk: everything Ritik encounters — links, articles, tweets, saved notes, the index layer of his Obsidian vault — gets captured into one place, auto-tagged, and stays findable by meaning later.

The fork's reason to exist: the stock web UI renders ported/crawled content out of proportion (giant headings, oversized cards) and reads as a generic bookmark manager. The fork makes the web app visually proportional and pleasant for the capture-first workflow Ritik actually lives in.

## Positioning

Capture-first personal library: capture is the job to be excellent at (web clipper, share sheet, chat-initiated saves via Donna); finding and reading serve capture. Karakeep upstream describes itself as "bookmark-everything for data hoarders"; this instance's distinguishing position is the closed loop it runs in — Karakeep ↔ Obsidian sync both directions, Donna saves/searches on Ritik's behalf from chat. A stock Karakeep deployment could not truthfully copy that.

## Operating Context

- Runs on a small VPS (Ubuntu 24.04, ~3.8 GB RAM) at `https://bookmarks.ritikpatni.me` via Cloudflare Tunnel; also reachable at http://localhost:3000 on-host
- Production deployment: Docker Compose at `/opt/karakeep` (web + chrome crawler + meilisearch); fork deployment swaps the image line only
- Fork repo: `/root/karakeep-fork` (branch `ui/ritik-compact`, GHCR image target `ghcr.io/notritikpatni/karakeep`)
- AI tagging: Ollama cloud (`glm-5.3-flash` for text inference) via the OpenAI-compatible endpoint
- Companion automation: hoarder-sync Obsidian plugin (hourly, vault direction) and the karakeep CLI (0.33.2, authed), plus a documented REST surface

## Capabilities and Constraints

Confirmed capabilities: link/text/asset bookmarks, AI auto-tagging (live, verified), full-text + search query language, lists (manual + smart), highlights, RSS import, REST API + CLI, browser/phone capture clients.

Confirmed constraints (durable):

- **No personal content ever.** The private Obsidian layer (555 files: jobs, people, medical, finances, planners) never enters Karakeep. Karakeep is the knowledge layer only; the personal-content boundary was enforced during import and must outlive any future import/sync work.
- **Upstream-mergeability is a preference, not a promise.** The fork diverges in `apps/web` UI as needed; rebase cadence is chosen per-release, not guaranteed.
- **Branding stays Karakeep.** The fork tunes the UI; it does not rebrand. Karakeep name/logos remain visible in the forked UI.
- Single server, currently ~16 GB disk free after cleanup; storage growth comes from crawled assets — watched at storage reviews.

## Brand Commitments

- Karakeep branding remains in the UI (confirmed Oct 14, fork included).
- Domain: `bookmarks.ritikpatni.me` under ritikpatni.me.

## Evidence on Hand

- 169 live bookmarks (imported from the non-personal Obsidian folders), AI-tagged 169/169, organized into 5 lists mirroring vault folders
- Obsidian vault import + 7-pass sanitization receipts live in the `karakeep` skill (artifacts reduced to zero)
- Working capture clients verified: web UI, CLI (`karakeep` on PATH), Obsidian sync plugin (PR #496)

## Product Principles

1. **Capture is the primary job.** Every UI and workflow decision is justified by how it improves getting content IN; finding and reading serve capture.
2. **The knowledge layer only.** Personal life (jobs, people, health, money) never appears in Karakeep — not in bookmarks, tags, or syncs.
3. **Proportion before decoration.** The web UI's core defect is scale mismatch (giant headings, oversized cards); the fork's aesthetic mandate is proportion, not new decoration.
4. **Stock brain, tuned body.** Backend, API, tagging pipeline, and infra stay stock/upstream; the fork concentrates divergence in the web UI layer.
5. **Closed loop.** Capture from any surface (web, phone, chat) must land in both Karakeep and the Obsidian knowledge layer without manual filing.

## Accessibility & Inclusion

No product-specific requirements established. Standard web accessibility (keyboard operation, contrast, semantic markup) applies as baseline; no confirmed special needs this iteration.