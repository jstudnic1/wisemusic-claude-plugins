---
name: wisemusic-weekly-artist-status
description: >-
  Use when someone at Wisemusic prepares the weekly status for an act with 360° services (concert
  management, PR, career development), or asks what is happening around one act: shows, releases,
  campaigns, merch, tasks, decisions and open problems, then a draft for the act in plain words.
  Workflow status-umelce of the first slice. Czech triggers include týdenní status, status pro
  umělce, co se děje u umělce, přehled umělce, report pro kapelu, 360, co nás čeká, plán na týden,
  co potřebujeme od umělce.
---

# Weekly status for a 360° act (status-umelce)

**Owner:** owner (the co-founders). **Used by:** owner, booking, pr, digital.

Answer in Czech unless the person writes in another language. The status is a draft for a person
to check and send (e-mail or a message); you never send anything.

1. **Which act.** If the person names none, `query_metric` `artist_overview` and offer the acts
   whose services include `360`, with their next show, next release, running campaigns and open
   problems. Otherwise `search` object_type artist and use the exact id.
2. **The card.** `get` the artist: status, services, who looks after the act, decisions, commitments,
   open questions and sources. Open the act's KB page from the card's sources with `sources` (source
   id) for how the act wants to be informed (tone, channel, how often); if there is none, ask the
   person.
3. **Everything around the act.** `query_metric` `artist_activity` with the artist_id: shows of the
   last 30 days and ahead, releases, campaigns, merch and open tasks, by date. `get` the shows of the
   coming 14 days and the next release for their details and open problems.
4. **What changed this week.** `timeline` on the artist with date_from 7 days back for decisions,
   documents and status changes; `related` from the artist with link meeting_artist for meetings,
   and read with `sources` only the parts about this act. What was said is not agreed: only
   decisions and commitments count.
5. **Draft the status** in the act's tone, four short blocks:
   - Co se za týden stalo: shows played, releases out, campaigns started or finished, decisions;
     only what the tools returned.
   - Co nás čeká: the next 14 days of shows (date, city, event), release dates and campaign
     milestones; dates only from the cards.
   - Co potřebujeme od tebe: tasks waiting on the act and open questions (photos, approvals, a
     setlist, a decision on a date).
   - Na co si dát pozor: open problems in plain words (a show without a contract, a pitch that did
     not make it), with what Wisemusic is doing about each.
   No fees or deal terms in the draft unless an owner asks for them; nothing about how anyone at
   Wisemusic works.
6. **Below the draft, for the person only:** the sources with their as-of times and what is missing
   or doubtful: a show without a venue or rider status, a release without a distributor, a task
   without an owner, nothing recorded for the act in 14 days.
7. If the person takes part in the first slice, offer `wisemusic-log-pilot-measurement` (workflow
   status-umelce: from opening the act's materials to a status ready to send).

**The answer contains:** the draft status in the act's tone; under it, for the person, the sources
with as-of times and the list of gaps.

**Never:** put a date, a fee or a promise into the status that no tool result supports, or send it
to the act yourself.
