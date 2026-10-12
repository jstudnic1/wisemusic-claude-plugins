---
name: wisemusic-start-here-owner
description: >-
  Use on day one, or when one of Wisemusic's co-founders (vedení) asks what Claude can do for them,
  where to start, or which skills to use first. Triggers include "where do I start", "what can you
  do for me", "kde začít", "co umím", "přehled labelu", "co se děje u umělců", "co hoří", "start
  vedení". Shows what the owners can see and do, the five skills they use most, three questions to
  try today, how approvals work, and where to get help.
---

# Start here: leadership (owner)

**Owner:** the co-founders. **Used by:** owner.

1. Welcome the person in their language (Czech by default) and say in two or three lines what the
   owners can see and do (below). If they ask what exists, call `describe`.
2. Show the five skills table, starting with `wisemusic-co-je-noveho` ("co je nového"), and the
   Další skills line under it, and ask which one they want to try.
3. Offer the three first questions and run the one they pick, with the tools named.
4. If they want to change something, explain how approvals work for the owners (below) and follow
   the `propose-a-change` skill.
5. End with where to get help and the proficiency ladder line.

**The answer contains:** a short welcome, what the owners can see and do, the five-skill table and
the Další skills line, three questions to try today, how approvals work, where to get help, and the
ladder line.

**Never:** repeat an act's deal terms or a fee to someone who cannot see them, or read the first
slice's numbers as a judgement of a person; they measure processes.

## What you can see and do

| Capability | Owners |
| --- | --- |
| Roster, releases, bookings, campaigns, merch, tasks | Read everything; propose and approve |
| Booking fees and campaign budgets | Visible (fees also to booking and back office, budgets to PR and digital) |
| Artists' deals and their terms | Visible to the owners only (vedení); a change needs the other co-founder's approval |
| Meetings and their decisions | Those you attended or that were shared with vedení |
| First-slice measurement | Record your own runs; read the numbers and decide the next step |
| Approve requests | Every action; deal terms only the other co-founder |

## Your five skills

| Skill | Use it when | Example question |
| --- | --- | --- |
| `wisemusic-co-je-noveho` | What changed across the label since yesterday, by act, each line with its source; what is waiting for you | "Co je nového?" |
| `wisemusic-weekly-artist-status` | The weekly status for a 360° act, or what is happening around one act | "Připrav týdenní status pro Lunu Vlny." |
| `wisemusic-booking-inquiry-to-offer` | An inquiry came in, an offer is waiting, a show needs its contract | "Přišla poptávka na Kováře do Brna, co s tím?" |
| `wisemusic-meeting-to-tasks` | After the weekly meeting or a meeting with an act: decisions and tasks | "Zpracuj středeční poradu." |
| `wisemusic-log-pilot-measurement` | How the first slice is going, or recording your own run | "Jak jde měření bookingu?" |

**Další skills** (from day one, no new integration): `wisemusic-trideni-posty` sorts your inbox with
your own mail connector in Claude ("Roztřiď mi poštu od pátku."); `wisemusic-ton-komunikace` writes
down how Wisemusic sounds or rewrites a text in it ("Sepiš, jak Wisemusic píše na sítích.").

## Three questions to try today

1. "Co se děje u kterého umělce?" Call `query_metric` `artist_overview`.
2. "Kolik máme v bookingu a za kolik?" Call `query_metric` `booking_pipeline_fees`.
3. "Co hoří?" Call `query_metric` `open_problems`, then `get` the objects it names.

## How approvals work for you

- You may approve every action in the approval portal, your own requests included, except an act's
  deal terms (`propose_action` `upsert_artist_deal`): the other co-founder approves those.
- Roster changes (`propose_action` `upsert_artist`, `propose_action` `set_artist_status`) and
  campaign budgets (`propose_action` `set_campaign_budget`) wait for one of you.
- Bookings are usually approved by whoever books, releases by digital, invoices by back office; step
  in when they are away or when the decision is yours (a fee below the act's usual one, a release
  date).
- A change is done only when `action_status` shows executed.

## Where to get help

- Booking, releases and PR processes: the person who owns each (the start-here skills of booking,
  digital and pr).
- System questions, access, anything broken: the system owner (Delta until the handover).
- Got stuck? Add it to the friction log (`discovery/friction-log.md`) or tell a champion; fixes
  ship the same week where possible.

## Your level

L0 ask questions; L1 use three skills and run actions with approval; L2 write a skill for your
own work (pair once with a champion); L3 own a routine (build one with Claude Code and ship it
through review).
