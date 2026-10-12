---
name: wisemusic-start-here-pr
description: >-
  Use on day one, or when someone in PR and media at Wisemusic asks what Claude can do for them,
  where to start, or which skills to use first. Triggers include "where do I start", "what can you
  do for me", "kde začít", "co umím", "PR", "média", "kampaně", "co vychází", "start PR". Shows
  what PR can see and do, the five skills PR uses most, three questions to try today, how approvals
  work, and where to get help.
---

# Start here: PR and media (pr)

**Owner:** the PR champion. **Used by:** pr.

1. Welcome the person in their language (Czech by default) and say in two or three lines what PR
   can see and do (below). If they ask what exists, call `describe`; it also shows the booking role
   if they book too.
2. Show the five skills table, starting with `wisemusic-co-je-noveho` ("co je nového"), and the
   Další skills line under it, and ask which one they want to try.
3. Offer the three first questions and run the one they pick, with the tools named.
4. If they want to change something, explain how approvals work for PR (below) and follow the
   `propose-a-change` skill.
5. End with where to get help and the proficiency ladder line.

**The answer contains:** a short welcome, what PR can see and do, the five-skill table and the Další
skills line, three questions to try today, how approvals work, where to get help, and the ladder
line.

**Never:** give the media a release date, a show or a fact that is still under embargo or that no
card or decision supports.

## What you can see and do

| Capability | PR |
| --- | --- |
| Roster, releases, bookings, merch | Read (release dates are embargoed until announced: inside the team only) |
| Campaigns | Read; propose and approve (PR, digital, playlist, ads) |
| Campaign budgets | Visible to PR, digital and the owners; only an owner approves a budget |
| Media outlets and other organizations | Read; propose new cards (outlets only; journalists' contacts stay in the press list) |
| Booking fees | Visible only if you also hold the booking role |
| Approve requests | Campaigns, organizations and tasks |

## Your five skills

| Skill | Use it when | Example question |
| --- | --- | --- |
| `wisemusic-co-je-noveho` | What changed around your acts, releases and campaigns since yesterday, each line with its source | "Co je nového u Míry Soula?" |
| `wisemusic-pr-campaign-brief` | A release or a show needs a PR campaign and its brief | "Připrav PR brief k albu Míry Soula." |
| `wisemusic-weekly-artist-status` | What is happening around an act before you talk to the media | "Co má Stará pošta v říjnu?" |
| `wisemusic-meeting-to-tasks` | After a meeting with an act or a medium | "Zpracuj schůzku s Lunou Vlny." |
| `cite-and-verify` | Before a fact goes into a press release | "Odkud je datum vánočního koncertu?" |

**Další skills** (from day one, no new integration): `wisemusic-ton-komunikace` writes down how
Wisemusic sounds or rewrites a text in it ("Přepiš tuhle tiskovou zprávu naším stylem.");
`wisemusic-trideni-posty` sorts your inbox with your own mail connector in Claude ("Co ode mě chtějí
média za víkend?").

## Three questions to try today

1. "Jaké kampaně běží a co nás čeká?" Call `query_metric` `campaign_calendar`.
2. "Co vychází v příštích týdnech?" Call `query_metric` `release_calendar`.
3. "Které koncerty můžeme ohlásit?" Call `query_metric` `upcoming_bookings` and keep the
   contract_signed ones (a confirmed show without a contract is not announced yet: assumption to
   confirm in the PR interview).

## How approvals work for you

- You propose and approve `propose_action` `upsert_campaign` and `propose_action`
  `set_campaign_status`, yours included.
- A budget (`propose_action` `set_campaign_budget`) waits for an owner.
- Media outlets: `propose_action` `upsert_organization` with kind media.
- A change is done only when `action_status` shows executed.

## Where to get help

- The PR process: the KB page "PR proces" (`sources` with that query) and the PR champion.
- System questions, access, anything broken: the system owner.
- Got stuck? Add it to the friction log (`discovery/friction-log.md`) or tell the champion; fixes
  ship the same week where possible.

## Your level

L0 ask questions; L1 use three skills and run actions with approval; L2 write a skill for your
own work (pair once with a champion); L3 own a routine (build one with Claude Code and ship it
through review).
