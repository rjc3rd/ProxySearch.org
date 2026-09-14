# PROJECT.md — ProxySearch (proxysearch.org)

Backfilled 2026-09-12 from the existing `README.md`/`INFRASTRUCTURE.md`,
since this project predates `PROJECT.md` existing. Review and correct
anything below.

## What this is

A privacy-respecting, JavaScript-free meta search engine that fetches
results from major US search providers without tracking. Started as a fork
of [Ahwxorg/LibreY](https://github.com/Ahwxorg/LibreY); diverged far enough
(full backend rewrite, ground-up Tailwind v4 redesign) that it's now its own
independent project, not upstream-tracked.

## Domain

proxysearch.org

## Goal

Reliability, first and foremost — "search, get nothing, search again, maybe
get something" was the exact failure mode that got the original build
abandoned for years. The whole point of the rewrite is a search that
actually returns real, relevant results on the first try, fast (currently
under a second, vs. the old build's ~10 seconds).

## Audience

Privacy-conscious search users who want a real, working meta-search proxy —
not a tech demo or a theme showcase.

## Must-haves

- Text search only, across engines individually re-verified to actually work
  from this server (currently DuckDuckGo, Bing, Yahoo)
- Mandatory SafeSearch, no visitor toggle
- Dark/light purely via `prefers-color-scheme`, no manual toggle
- Fast, no-JS-required core search flow

## Non-goals

- Image/video search — removed entirely; every backend tried
  (Invidious/Qwant/DuckDuckGo image API/Yahoo/Bing) failed or actively
  blocked scraping in production testing. May come back if a provider
  becomes reliably scrapeable again.
- Fallback to other LibreY/LibreX instances — removed; sending a visitor's
  raw query to a third-party server outside this project's control is
  exactly the kind of privacy leak this project exists to avoid.
- The old ~19-theme picker (Dracula, Nord, Tokyo Night, Catppuccin, etc.) —
  removed outright, nobody used it and it wasn't particularly attractive.

## Design direction

Real Tailwind CSS v4 rebuild (not a reskin) — mobile-first, one consistent
accent color, proper shadows/rounded corners, no CDN (locally compiled
build). Exactly two visual states, dark and light, chosen automatically from
the visitor's own system setting.

## Copy voice

Direct and honest about tradeoffs and limitations — the README itself
models this (e.g. openly documenting *why* Google/Brave/image search were
dropped, rather than silently omitting them). Not a marketing-driven tone.

## Known constraints

- **Standing authorization (added 2026-09-07):** the one site with
  authorization to write code and deploy (`./deploy-site`) autonomously,
  without asking first each time — every other site in this family still
  requires asking before code changes and always before deploying. Weekly
  check-in cadence — see `INFRASTRUCTURE.md`.
- AGPL-3.0 license, same as upstream — credit to Ahwxorg/LibreY for the
  original foundation.
- GitHub deploy key is now account-wide (also covers PrivacyOS).

## Inspiration / prior art

The original [LibreY](https://github.com/Ahwxorg/LibreY) project — this
project's starting point, though the relationship is now closer to
"Ubuntu to Debian," maybe further apart than that.

## Anything already decided

- Engine roster is deliberately smaller than upstream's default five
  (Google/Brave/Startpage/Ask.com all evaluated and rejected for concrete,
  verified technical reasons — active bot blocks or the provider shutting
  down entirely) — don't pad the list back out with engines that don't
  actually work just to hit a round number.
- This is the actively "vibe coded" site going forward — the one place
  autonomous iteration is the expected working mode, not the exception.
