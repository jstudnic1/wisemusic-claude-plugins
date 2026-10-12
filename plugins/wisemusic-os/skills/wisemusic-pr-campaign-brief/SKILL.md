---
name: wisemusic-pr-campaign-brief
description: >-
  Use when a release, a show or a tour at Wisemusic needs a PR campaign: drafts the brief (goal, key
  message, story hooks, assets, embargo, target outlets, timeline back from the release or the show,
  what success means), proposes the campaign and its tasks, and the budget for an owner to approve.
  Also for playlist and ads campaigns alongside PR. Czech triggers include PR kampaň, PR brief,
  mediální plán, tisková zpráva, press kit, rozhovor, média, PR k singlu, PR k albu, PR ke koncertu,
  ohlášení koncertu, embargo, kampaň k vydání.
---

# PR campaign brief

**Owner:** pr (the PR champion). **Used by:** pr, digital, owner.

Answer in Czech unless the person writes in another language. Release dates and shows that are not
announced yet are under embargo: the brief says until when, and nothing leaves the team before.

1. **What the campaign is for.** `search` the act, and the release or the show; `get` each card
   (release date, status, pitch; show date, city, contract). A show is announced only when its
   contract is signed (assumption to confirm with PR); say so if it is not.
2. **What already runs.** `query_metric` `campaign_calendar` and `query_metric` `artist_activity` for
   the act: campaigns planned or running, other releases and shows that compete for attention.
3. **The PR process.** Read the KB page "PR proces" (`sources` with that query) and the act's KB page
   for its story, tone and what it does not talk about.
4. **Draft the brief**, one page:
   - Cíl: what should change (an announcement heard, a show sold, a release in the media); no promised
     numbers.
   - Hlavní sdělení and two or three story hooks, from the cards and the KB only.
   - Podklady: photos, press kit, video, quotes from the act; what exists (sources) and what to get.
   - Embargo: until which date, and who may break it (an owner).
   - Média: outlets by `search` object_type organization with kind media; outlets only, never a
     journalist's name or contact (they stay in the press list).
   - Časový plán: dated steps counted back from the release or the show.
   - Co je úspěch: what will be counted afterwards (interviews, reviews, mentions), marked as the PR
     person's measure.
5. **Propose the campaign.** `propose_action` `upsert_campaign` with campaign_id `<release_id or
   artist_id>-<kind>`, artist_id, release_id if any, kind (pr, digital, playlist, ads), title,
   start_date and end_date as agreed, status `planned` and owner. PR, digital or an owner approves.
6. **Budget.** Only when the person gives an amount: `propose_action` `set_campaign_budget` with
   campaign_id and budget (CZK without VAT); an owner approves it, and the preview never shows the
   amount.
7. **Tasks.** With the person's agreement, for each step `propose_action` `create_task` with task_id
   `<campaign_id>-<step slug>`, campaign_id and artist_id, owner and due_date only if agreed. Check
   every proposal with `action_status`.

**The answer contains:** the brief as Markdown, the embargo date, each proposal's preview, request
id and status, and what is still missing (assets, a decision, a budget).

**Never:** name a journalist or a contact, send anything to the media, or let an embargoed date or
an unsigned show into a text meant for the outside.
