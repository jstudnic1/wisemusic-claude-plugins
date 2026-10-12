---
name: wisemusic-start-here-digital
description: >-
  Use on day one, or when someone in digital at Wisemusic (distribution, playlists, the platforms'
  tools, socials, ads) asks what Claude can do for them, where to start, or which skills to use
  first. Triggers include "where do I start", "what can you do for me", "kde začít", "co umím",
  "vydání", "distribuce", "pitch", "playlisty", "reklama", "start digitál". Shows what digital can
  see and do, the five skills digital uses most, three questions to try today, how approvals work,
  and where to get help.
---

# Start here: digital

**Owner:** the digital champion. **Used by:** digital.

1. Welcome the person in their language (Czech by default) and say in two or three lines what
   digital can see and do (below). If they ask what exists, call `describe`; it also shows the
   booking role if they book too.
2. Show the five skills table, starting with `wisemusic-co-je-noveho` ("co je nového"), and the
   Další skills line under it, and ask which one they want to try.
3. Offer the three first questions and run the one they pick, with the tools named.
4. If they want to change something, explain how approvals work for digital (below) and follow
   the `propose-a-change` skill.
5. End with where to get help and the proficiency ladder line.

**The answer contains:** a short welcome, what digital can see and do, the five-skill table and the
Další skills line, three questions to try today, how approvals work, where to get help, and the
ladder line.

**Never:** say a release was delivered or pitched when the card does not show it, or quote
streaming numbers: Company OS does not hold them (the platforms' dashboards do).

## What you can see and do

| Capability | Digital |
| --- | --- |
| Releases | Read; propose and approve (plan, status, master, cover, pitch) |
| Campaigns (digital, playlist, ads) | Read; propose and approve; budgets visible, approved by an owner |
| Roster, bookings, merch | Read; propose merch products (back office approves) |
| Distributor and other organizations | Read; propose new cards |
| Booking fees | Visible only if you also hold the booking role |
| Approve requests | Releases, campaigns, organizations and tasks |

## Your five skills

| Skill | Use it when | Example question |
| --- | --- | --- |
| `wisemusic-co-je-noveho` | What changed around releases and campaigns since yesterday, and what is waiting for you | "Co je nového u vydání?" |
| `wisemusic-release-plan` | A release from master to release day, or what is late | "Naplánuj vydání singlu Sklo na 19. 10." |
| `wisemusic-pr-campaign-brief` | A playlist or ads campaign alongside the PR brief | "Připrav playlistovou kampaň k Půlnoci." |
| `wisemusic-weekly-artist-status` | What is happening around an act | "Co se děje u Kováře MC?" |
| `wisemusic-log-pilot-measurement` | You timed a release-plan run for the first slice | "Zapiš měření: plan-vydani, assisted." |

**Další skills** (from day one, no new integration): `wisemusic-ton-komunikace` writes down how
Wisemusic sounds or rewrites a text in it ("Sedí tenhle post na nás?"); `wisemusic-trideni-posty`
sorts your inbox with your own mail connector in Claude ("Co mi za víkend napsal distributor?").

## Three questions to try today

1. "Co vychází a co k tomu chybí?" Call `query_metric` `release_calendar`.
2. "Kde nestíháme pitch nebo podklady?" Call `query_metric` `open_problems` and keep the
   release_pitch_missing and release_assets_missing rows.
3. "Jaké kampaně běží?" Call `query_metric` `campaign_calendar`.

## How approvals work for you

- You propose and approve `propose_action` `upsert_release`, `propose_action` `set_release_status`
  and `propose_action` `update_release_checklist`, yours included; an owner may too.
- Campaigns: `propose_action` `upsert_campaign`, `propose_action` `set_campaign_status`; budgets
  (`propose_action` `set_campaign_budget`) wait for an owner.
- Merch products you propose are approved by back office or an owner.
- A change is done only when `action_status` shows executed.

## Where to get help

- The release checklist: the KB page "Checklist vydání" (`sources` with that query) and the digital
  champion.
- System questions, access, anything broken: the system owner.
- Got stuck? Add it to the friction log (`discovery/friction-log.md`) or tell the champion; fixes
  ship the same week where possible.

## Your level

L0 ask questions; L1 use three skills and run actions with approval; L2 write a skill for your
own work (pair once with a champion); L3 own a routine (build one with Claude Code and ship it
through review).
