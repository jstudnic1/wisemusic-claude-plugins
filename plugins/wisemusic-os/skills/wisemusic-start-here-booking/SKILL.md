---
name: wisemusic-start-here-booking
description: >-
  Use on day one, or when someone at Wisemusic who books shows asks what Claude can do for them,
  where to start, or which skills to use first. At Wisemusic several people book (the Contacts page lists the CEO, PR and digital), so this is for every
  booker whatever their main role. Triggers include "where do I start", "what can you do for me",
  "kde začít", "co umím", "moje koncerty", "booking", "poptávky", "co je v bookingu", "start
  booking". Shows what booking can see and do, the five skills a booker uses most, three questions
  to try today, how approvals work, and where to get help.
---

# Start here: booking

**Owner:** the booking champion (assumption: the CEO, the co-founder the Contacts page lists for booking). **Used by:** booking.

1. Welcome the person in their language (Czech by default) and say in two or three lines what a
   booker can see and do (below). If they ask what exists, call `describe`; it also shows their
   other role (pr, digital, ops or owner), because the booking role comes on top of it.
2. Show the five skills table, starting with `wisemusic-co-je-noveho` ("co je nového"), and the
   Další skills line under it, and ask which one they want to try.
3. Offer the three first questions and run the one they pick, with the tools named.
4. If they want to change something, explain how approvals work for booking (below) and follow
   the `propose-a-change` skill.
5. End with where to get help and the proficiency ladder line.

**The answer contains:** a short welcome, what a booker can see and do, the five-skill table and the
Další skills line, three questions to try today, how approvals work, where to get help, and the
ladder line.

**Never:** tell a promoter a fee, a date or a line-up that no booking card or decision supports,
or confirm a show on the act's behalf.

## What you can see and do

| Capability | Booking |
| --- | --- |
| Roster (artists) | Read; propose changes (the owners approve) |
| Bookings | Read all; propose and approve (yours included) |
| Booking fees | Visible to booking, back office and the owners |
| Releases, campaigns, merch | Read (to plan shows around release days and campaigns) |
| Promoters, venues, festivals | Read; propose and approve new cards (no personal contacts) |
| Artists' deal terms, campaign budgets | Not visible (owners; owners, PR and digital) |
| Approve requests | Bookings, the rider status, organizations and tasks |

## Your five skills

| Skill | Use it when | Example question |
| --- | --- | --- |
| `wisemusic-co-je-noveho` | What changed around your shows and acts since yesterday, and what is waiting for you, each line with its source | "Co je nového v bookingu?" |
| `wisemusic-booking-inquiry-to-offer` | An inquiry came in, an offer waits for an answer, a show needs its contract and rider | "Přišla poptávka na Neon Pastvinu do Ostravy 28. 11." |
| `wisemusic-weekly-artist-status` | What is happening around one act before you answer a promoter | "Co má Luna Vlny v listopadu?" |
| `wisemusic-meeting-to-tasks` | After the weekly booking meeting | "Zpracuj poznámky z porady." |
| `wisemusic-log-pilot-measurement` | You timed an inquiry-to-offer run for the first slice | "Zapiš měření: booking-nabidka, baseline, 25 + 5 + 0 + 5 min." |

**Další skills** (from day one, no new integration): `wisemusic-trideni-posty` sorts your inbox with
your own mail connector in Claude ("Jaké poptávky mi přišly od pátku?"); `wisemusic-ton-komunikace`
writes down how Wisemusic sounds or rewrites a text in it ("Přepiš tuhle nabídku pořadateli naším
stylem.").

## Three questions to try today

1. "Které koncerty máme v příštích dvou měsících?" Call `query_metric` `upcoming_bookings`.
2. "Na které nabídky nám ještě nikdo neodpověděl?" Call `query_metric` `booking_pipeline`, then
   `query_metric` `open_problems` and keep the booking_offer_no_answer rows.
3. "Co ještě chybí ke koncertům v příštích 14 dnech?" Call `query_metric` `open_problems` (contract,
   rider) and `get` each booking it names.

## How approvals work for you

- You propose and approve `propose_action` `upsert_booking` (the only action with the fee),
  `propose_action` `set_booking_status` and `propose_action` `set_booking_tech`; another booker or
  an owner may approve, and so may you.
- Invoices and payments (`propose_action` `record_booking_invoice`) are approved by back office or
  an owner.
- Roster changes go to the owners (`propose_action` `upsert_artist`).
- A change is done only when `action_status` shows executed.

## Where to get help

- How booking works at Wisemusic: the KB page "Jak funguje booking" (`sources` with that query) and
  the booking champion.
- System questions, access, anything broken: the system owner.
- Got stuck? Add it to the friction log (`discovery/friction-log.md`) or tell the champion; fixes
  ship the same week where possible.

## Your level

L0 ask questions; L1 use three skills and run actions with approval; L2 write a skill for your
own work (pair once with a champion); L3 own a routine (build one with Claude Code and ship it
through review).
