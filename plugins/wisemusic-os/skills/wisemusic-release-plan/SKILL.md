---
name: wisemusic-release-plan
description: >-
  Use when a single, EP or album is coming at Wisemusic and someone needs its release plan: from the
  final master and the cover through delivery to the distributor and the platform pitch to release
  day and the week after; also to check what is late across all upcoming releases. Workflow
  plan-vydani of the first slice. Czech triggers include plán vydání, nový singl, vydání, datum
  vydání, release, master, mastering, obal, cover, metadata, distributor, dodání, pitch, Spotify for
  Artists, playlisty, pre-save, release day, co chybí k vydání.
---

# Release plan: from master to release day (plan-vydani)

**Owner:** digital (the digital champion). **Used by:** digital, owner, ops, pr.

Answer in Czech unless the person writes in another language. Unannounced titles and dates are
under embargo: they stay inside the team.

1. **Which release.** `query_metric` `release_calendar`: every release from 30 days back, with days
   to release, status, master, cover, pitch and distributor. If the person names one, `search`
   object_type release and `get` the card; if it does not exist yet, go to step 2, otherwise step 3.
2. **A new release.** `search` object_type artist for the act. `propose_action` `upsert_release`
   with release_id `<artist_id>-<title slug>`, artist_id, title, kind (single, ep, album),
   release_date as the person gives it (the release date is a decision of the act and the owners:
   never propose one yourself), status `planning`, master_status, cover_status and pitch_status as
   they are, distributor_id (`search` object_type organization, kind distributor) and owner. Digital
   or an owner approves.
3. **The plan, backwards from release day.** Read the KB page "Checklist vydání" (`sources` with
   that query) and lay out its steps with real dates counted back from release_date. Where the page
   states no lead time, use these drafts and say they are assumptions to confirm: final master and
   cover 28 days before, delivery to the distributor 21 days before, the editorial pitch through the
   platforms' tools no later than 7 days before (Spotify takes pitches only before release; 3 to 4
   weeks before is better), pre-save and social assets 14 days before, PR and playlist campaigns
   (`query_metric` `campaign_calendar`), release day, a report 7 days after. Mark every step already
   past its date.
4. **Tasks.** With the person's agreement, for each open step `propose_action` `create_task` with
   task_id `<release_id>-<step slug>`, release_id, artist_id, status `todo`, owner only if someone
   agreed, due_date = the step's date only if the person agrees to it, and source `manual` or the KB
   page. Check `query_metric` `artist_activity` first so you do not duplicate a task.
5. **Keep the card true.** When the person reports progress: `propose_action`
   `update_release_checklist` with master_status, cover_status and pitch_status as they are now (all
   three, read from the card); `propose_action` `set_release_status` with `mastering`, `delivered`
   (with delivered_on) or `released`. Check every proposal with `action_status`.
6. **What is late.** `query_metric` `open_problems` and keep release_pitch_missing (a release within
   8 days without a finished pitch) and release_assets_missing (within 14 days without a ready master
   or cover). For a missed pitch, say plainly that editorial playlists are probably out for this
   release and list what is still possible (the act's own channels, playlist and ads campaigns),
   without promising results.
7. If the person takes part in the first slice, offer `wisemusic-log-pilot-measurement` (workflow
   plan-vydani: from opening the release to a plan with dates and tasks).

**The answer contains:** the release card (status, days to release, master, cover, pitch,
distributor), the plan as a dated list with what is done, open or late, each proposal's preview,
request id and status, and the assumptions about lead times that still need confirming.

**Never:** propose or announce a release date nobody decided, say a pitch was submitted or a
release delivered when the person did not confirm it, or quote streaming numbers.
