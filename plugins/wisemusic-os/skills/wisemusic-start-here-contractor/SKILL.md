---
name: wisemusic-start-here-contractor
description: >-
  Use on day one, or when an external collaborator of Wisemusic (tour manager, sound engineer,
  photographer, designer) asks what Claude can do for them, where to start, or what they can see.
  Triggers include "where do I start", "what can you do for me", "kde začít", "co umím", "co vidím
  jako externista", "umělci labelu", "jak to u vás chodí", "start externista". Shows what contractors
  can see and do, the skills they use, three questions to try today, how changes are made, and where
  to get help.
---

# Start here: contractor (externista)

**Owner:** the back-office champion. **Used by:** contractor.

1. Welcome the person in their language (Czech by default) and say in two or three lines what a
   contractor can see and do (below). If they ask what exists, call `describe`.
2. Show the five skills table, starting with `wisemusic-co-je-noveho` ("co je nového"), and ask
   which one they want to try.
3. Offer the three first questions and run the one they pick, with the tools named.
4. If they need a change, explain that the person at Wisemusic who brought them in makes it.
5. End with where to get help and the proficiency ladder line.

**The answer contains:** a short welcome, what a contractor can see and do, the five-skill table,
three questions to try today, how changes are made, where to get help, and the ladder line.

**Never:** tell a contractor that a show or a release does not exist when it is only hidden from
them, or pass on anything from one act's work to another.

## What you can see and do

| Capability | Contractor |
| --- | --- |
| The roster (acts, genres, services, who looks after each) | Read |
| The knowledge base (how booking, releases and PR work; checklists) | Read |
| Bookings, releases, campaigns, merch, organizations, tasks | Not visible for now; the person who brought you in shares what you need (the core cannot share one show with one tour manager yet) |
| Meetings | Only those shared with you |
| First-slice measurement | Record your own runs if you take part |

## Your five skills

| Skill | Use it when | Example question |
| --- | --- | --- |
| `wisemusic-co-je-noveho` | What is new on the roster and in what you may see, each line with its source | "Co je nového?" |
| `company-os-basics` | Any question about what you can look up and how | "Co tady najdu?" |
| `cite-and-verify` | Before you rely on a rule or a checklist | "Kde je napsané, co patří do rideru?" |
| `capture-a-decision` | A decision from a meeting you were part of should be recorded | "Domluvili jsme pořadí setu, zapiš to." |
| `wisemusic-log-pilot-measurement` | You take part in the first slice and timed a run | "Zapiš měření." |

## Three questions to try today

1. "Co tady vidím?" Call `describe`.
2. "Které umělce Wisemusic zastupuje?" Call `search` with object_type artist.
3. "Co patří do technického rideru?" Call `sources` with the query "Jak funguje booking".

## How changes are made

- You may record your own measurement with `propose_action` `log_pilot_observation` and approve it
  yourself.
- Shows, releases, campaigns and tasks are changed by Wisemusic's staff: tell the person who brought
  you in.
- A change is done only when `action_status` shows executed.

## Where to get help

- Your show or job and your access: the person at Wisemusic who brought you in.
- System questions, anything broken: the system owner.
- Got stuck? Tell the person who brought you in; it goes into the friction log
  (`discovery/friction-log.md`).

## Your level

L0 ask questions; L1 use three skills and run actions with approval; L2 write a skill for your
own work (pair once with a champion); L3 own a routine (build one with Claude Code and ship it
through review).
