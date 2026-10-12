---
name: wisemusic-start-here-ops
description: >-
  Use on day one, or when someone in Wisemusic's back office and production asks what Claude can do
  for them, where to start, or which skills to use first. Triggers include "where do I start",
  "what can you do for me", "kde začít", "co umím", "smlouvy", "rider", "faktury", "co nevyfakturovat",
  "merch", "produkce", "start back office". Shows what back office can see and do, the five skills it
  uses most, three questions to try today, how approvals work, and where to get help.
---

# Start here: back office and production (ops)

**Owner:** the back-office champion. **Used by:** ops.

1. Welcome the person in their language (Czech by default) and say in two or three lines what back
   office can see and do (below). If they ask what exists, call `describe`; it also shows the
   booking role if they book too.
2. Show the five skills table, starting with `wisemusic-co-je-noveho` ("co je nového"), and the
   Další skills line under it, and ask which one they want to try.
3. Offer the three first questions and run the one they pick, with the tools named.
4. If they want to change something, explain how approvals work for back office (below) and follow
   the `propose-a-change` skill.
5. End with where to get help and the proficiency ladder line.

**The answer contains:** a short welcome, what back office can see and do, the five-skill table and
the Další skills line, three questions to try today, how approvals work, where to get help, and the
ladder line.

**Never:** record an invoice as sent or a payment as received that the invoicing tool or the bank
does not show; Company OS never issues invoices.

## What you can see and do

| Capability | Back office (ops) |
| --- | --- |
| Bookings | Read; propose status changes (contract signed, played) and the rider status; record invoices and payments |
| Booking fees | Visible (you invoice them) |
| Releases | Read; propose status and checklist changes (digital approves the status) |
| Merch (SUPERSONIC SPEED) | Read; propose and approve |
| Tasks | Read; propose and approve; you keep the team's agenda (assumption) |
| Artists' deal terms, campaign budgets | Not visible |
| Approve requests | Invoices and payments, rider status, merch, release checklists, tasks |

## Your five skills

| Skill | Use it when | Example question |
| --- | --- | --- |
| `wisemusic-co-je-noveho` | What changed since yesterday across shows, releases, merch and tasks, and what is waiting for you | "Co je nového a co čeká na mě?" |
| `wisemusic-meeting-to-tasks` | After the weekly meeting: decisions and tasks with owners and dates | "Zpracuj středeční poradu." |
| `wisemusic-booking-inquiry-to-offer` | A confirmed show needs its contract, rider and invoice (steps 8 and 9) | "Co chybí ke koncertům příští týden?" |
| `wisemusic-release-plan` | Master, cover and delivery for a release | "Je Beton připravený k dodání?" |
| `cite-and-verify` | Before a date or a sum goes into a contract or an invoice | "Odkud je datum koncertu v Plzni?" |

**Další skills** (from day one, no new integration): `wisemusic-trideni-posty` sorts your inbox with
your own mail connector in Claude ("Roztřiď mi poštu a najdi faktury od dodavatelů.").

## Three questions to try today

1. "Co je po odehrání a ještě to není vyfakturované, a co je po splatnosti?" Call `query_metric`
   `open_problems` and keep the booking_not_invoiced and booking_invoice_overdue rows.
2. "Za kolik máme odehráno a nezaplaceno?" Call `query_metric` `booking_pipeline_fees`.
3. "Co je po termínu?" Call `query_metric` `overdue_tasks`, then `query_metric` `merch_pipeline`.

## How approvals work for you

- You decide here in Claude, never in a portal: Claude shows the preview and asks "Potvrdit?"; your
  explicit "ano" approves it (`decide_action`), "ne" rejects it. "Co čeká na mé schválení?" lists
  what others proposed for you to decide (`my_approvals`), such as invoices booking recorded.
- You propose and approve `propose_action` `record_booking_invoice` (invoiced with its dates, paid),
  `propose_action` `set_booking_tech`, `propose_action` `upsert_merch_product`, `propose_action`
  `set_merch_status` and `propose_action` `update_release_checklist`, yours included.
- You propose `propose_action` `set_booking_status` (contract signed, played) and `propose_action`
  `set_release_status`; a booker or digital approves in their own Claude.
- A change is done only when `action_status` shows executed.

## Where to get help

- Contracts, riders and invoices: the KB page "Jak funguje booking" and the back-office champion.
- System questions, access, anything broken: the system owner.
- Got stuck? Add it to the friction log (`discovery/friction-log.md`) or tell the champion; fixes
  ship the same week where possible.

## Your level

L0 ask questions; L1 use three skills and run actions with approval; L2 write a skill for your
own work (pair once with a champion); L3 own a routine (build one with Claude Code and ship it
through review).
