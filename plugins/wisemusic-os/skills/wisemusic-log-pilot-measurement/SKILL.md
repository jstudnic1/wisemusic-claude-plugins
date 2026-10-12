---
name: wisemusic-log-pilot-measurement
description: >-
  Use when someone at Wisemusic measuring the first slice wants to record one timed run of a
  workflow (an inquiry to an offer, a release plan, a weekly artist status), baseline without
  Claude or assisted with Claude, with the minutes they measured themselves; and when the owners ask
  how the measurement is going. Czech triggers include zapiš měření, měření, kolik minut, baseline,
  assisted, jak jde měření, vyhodnocení, týdenní review, první slice.
---

# Log a measurement of the first slice

**Owner:** owner (the co-founders, with the champion of the slice). **Used by:** everyone in the
first slice.

We measure repeated workflows, not people. Every record is entered by the person who did the work,
with real minutes; nobody is tracked passively. A result is an observation on a small sample, not
proof (kit/12, the two-week verification).

| Workflow | `workflow` | Measuring starts | Measuring ends | Done well means |
| --- | --- | --- | --- | --- |
| Poptávka → nabídka | `booking-nabidka` | opening the inquiry | the offer ready to send (not sent) | the date checked against the act's calendar, the fee as agreed, nothing missing |
| Plán vydání | `plan-vydani` | opening the release | a dated plan with tasks and the card up to date | every step has a date, nothing late is missed |
| Týdenní status umělce | `status-umelce` | opening the act's materials | the status ready to send | facts match the cards, nothing important missing |

1. **Only on an explicit request, only measured minutes.** The person gives: workflow, method
   (`baseline` without Claude, `assisted` with Claude), minutes of work (`work_min`), verification
   (`verify_min`, checking facts and sources), fixes (`fix_min`, rework after their own check or a
   colleague's comment), support (`support_min`, time someone else had to help, theirs included),
   usable (the output was usable after ordinary edits), critical error (a wrong date, fee or venue
   that would harm an act or a partner, even if caught), hand-off (`continued`: a colleague carried
   on without questions, `failed`: they had to ask, `not_tested`), the date of the work and a task
   reference. If a value is missing, ask for it. If the person did not measure, nothing is recorded:
   never estimate, round or reconstruct minutes afterwards.
2. **The task reference** is internal, without names or contacts: `<booking_id>:nabidka`,
   `<release_id>:plan`, `<artist_id>:status:<ISO week>`. An optional note (at most 500 characters)
   may say what helped or what was missing, never anything about a person.
3. **The record id** must be new for every record, for example `<workflow>:<task reference>:<method>`
   (`booking-nabidka:kovar-mc-2026-11-21-brno:nabidka:baseline`), 8 to 120 characters of lowercase
   letters, digits and `. _ : -`. Recording again under an existing id replaces that record, so reuse
   an id only to correct the same record.
4. **Propose it:** `propose_action` `log_pilot_observation` with {observation_id, workflow, method,
   work_min, verify_min, fix_min, support_min, usable, critical_error, handoff, task_ref,
   observed_on, note}. Read the preview back to the person. They approve it themselves in the
   approval portal with one tap. Check with `action_status`: recorded only when it shows executed.
5. **How it is going:** `query_metric` `pilot_minutes_by_workflow` with date_from and date_to (read the
   second assisted week on its own: the first includes learning the tool). Per workflow and method it
   returns observations, median total minutes, share usable, critical errors, hand-offs and, for
   assisted runs, `time_saved_vs_baseline`. Read them against the first slice's targets
   (discovery/first-slice.md) and say how many records each workflow still needs (at least three
   baseline and three assisted runs).

**The answer contains:** the preview, request id and status of the record; for progress, the
metric's rows as returned with its definition, against the targets, and the note that it is an
observation on a small sample.

**Never:** estimate, round or fill in minutes the person did not measure, or record anything about
a person.
