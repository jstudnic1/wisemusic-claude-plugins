---
name: onboarding-interview
description: >-
  Use to run the onboarding AI interview with one employee and turn it into a role card.
  Triggers include "start my interview", "onboarding interview", "map my work", "role card",
  "rozhovor", "mapování práce", "karta role". Claude asks eight questions one at a time about
  tasks, systems, files, decisions, waiting and pain, reads the card back for the person to
  confirm, and outputs it as one Markdown block to save in the company's discovery folder. Works
  without the company connector.
---

# Onboarding interview

**Owner:** the system owner (whoever runs onboarding). **Used by:** every employee, once in
the first week, and again when their role changes.

A 30 to 45 minute conversation with one person. It produces one role card: their tasks, the
systems and files they use, the decisions they make, and candidate skills, rules, actions and
object types derived from those tasks. Everything you need is on this page; you do not need
the repository.

1. **Give the notice first, before any question.** Say it in the person's language (both
   versions are below) and wait for an OK.
2. **Set up the card.** Ask for their role as Company OS names it (the onboarding invitation
   says it, for example ops or sales), their team, their `person_ref` and today's date.
   `person_ref` is an id from the company's people list, such as `p-07` or `p-klara`; it does
   not have to be a name. If they have none, use the role plus a number (`p-ops-1`) and say the
   onboarding lead may rename the file.
3. **Ask the eight questions one at a time** (table below). Never put two questions in one
   message. Ask questions 3 to 5 per task, starting with the task that takes the most time;
   cover at most eight tasks.
4. **Probe vague answers**, at most twice per question, then move on (probes below). If the
   person says "skip", skip without comment.
5. **Leave out what does not belong** (list below). If the person raises it, say "I'll leave
   that out of the card" and continue.
6. **Optional, only if the company connector is connected:** call `describe` and map the
   systems, files and checks they mentioned to existing object types, actions and metrics.
   Note in a candidate's `why` when it already exists, for example "exists as action
   rental_create".
7. **Derive candidates from the tasks**, never from opinions about the person (rules below).
8. **Read the card back** in plain words: each task with cadence, inputs, outputs, decisions,
   systems and pain, then the candidates. Ask: "Is anything wrong, missing, or something you
   want removed?" Apply every change. Repeat until they say it is right.
9. **Output the card** only after they confirm: one Markdown code block in the format below,
   and the path to save it as: `instances/[company]/discovery/role-cards/[person_ref].md`.
   If they named private spreadsheets or files, suggest the `data-amnesty` skill next.

**The answer contains:** during the interview, one question per message; at the end, the
read-back, the person's confirmation, then the role card as a single Markdown code block and
the file path to save it under.

**Never:** judge or record how fast, how well or how much the person works, their tone, or
anything that compares them with colleagues.

## The notice

> This interview maps your work, not you. Nothing from it is used to evaluate you. At the end
> you read the role card and change anything before it is saved. You can skip any question.

> Tento rozhovor mapuje vaši práci, ne vás. Nic z něj se nepoužije k vašemu hodnocení. Na
> konci si kartu role přečtete a cokoli opravíte, než se uloží. Kteroukoli otázku můžete
> přeskočit.

## The eight questions

| # | Ask | Listen for (goes into the card) |
| --- | --- | --- |
| 1 | What does a normal week look like for you? Walk me through yesterday. | The task list |
| 2 | Which of these tasks repeat: daily, weekly, monthly, per order? What starts each one? | `cadence`; what starts it (body table) |
| 3 | For this task, what do you need before you start, and what do you hand over at the end? | `inputs`, `outputs` |
| 4 | Which systems, files and spreadsheets do you open for it, including private ones only you use? | `systems`; files for the data amnesty |
| 5 | Which decisions do you make in it? What do you check first? Who approves? | `decisions`; approver (body notes) |
| 6 | What do you wait for from colleagues or from outside the company? | Waiting on others (body notes) |
| 7 | Where does it get stuck or go wrong? What did the last time cost, in hours? | `pain`, `time_per_week_hours` |
| 8 | If an assistant could do one thing for you every morning, what would it be? | One thing every morning (body notes) |

Probes for vague answers:

- "Can you tell me about the last time that happened?"
- "What did you open first?"
- "What would happen if nobody did this for a week?"
- "Roughly how many hours a week does this task take?"
- "Who else needs the result?"

Hours are the person's own rough estimate of a task's size, used only to decide what to
automate first. Never record their total hours, pace, or how busy they are.

## What never goes on the card

- Speed, quality, workload, tone, mood, mistakes by a named person, or comparisons with
  colleagues.
- Customer personal data: no customer names, emails, phone numbers or addresses. Write "a
  customer".
- Health, HR, salary or family matters, even if the person mentions them.
- The contents of files. File names, where they live and their column headers are enough.

## Deriving candidates

| Candidate | Comes from | Name format |
| --- | --- | --- |
| `candidate_skills` | A task repeated with the same steps | lowercase-hyphen, e.g. `morning-stock-check` |
| `candidate_rules` | A check the person does by eye | lowercase_underscore, e.g. `negative_stock_without_preorder` |
| `candidate_actions` | A change the person makes by hand in a system | lowercase_underscore, e.g. `set_stock` |
| `candidate_object_types` | A thing they track that no system holds | lowercase_underscore, e.g. `stock_movement` |
| `open_questions` | Anything unclear, or a candidate with no decision behind it | a plain question |

Every candidate lists the `tasks` it came from, using the exact task names, and a short `why`.
A candidate may also be a plain string.

## Role card format

Keys are fixed and in English. Task names and notes may be in the interview's language. The
values below are an example.

````markdown
---
role: ops
team: warehouse
person_ref: p-klara
interviewed_on: 2026-10-01
example: false
tasks:
  - name: Morning stock check
    cadence: daily              # daily | weekly | monthly | per order | per event | ad hoc
    inputs: [WooCommerce stock, ATUM ledger]
    outputs: [list of SKUs to recount]
    decisions: [which SKUs to recount first]
    systems: [woocommerce, atum]
    pain: The two systems disagree and nobody knows which is right.
    time_per_week_hours: 3
candidate_skills:
  - {name: morning-stock-check, tasks: [Morning stock check], why: same steps every morning}
candidate_rules:
  - {name: negative_stock_without_preorder, tasks: [Morning stock check], why: checked by eye today}
candidate_actions:
  - {name: set_stock, tasks: [Morning stock check], why: corrected in WooCommerce by hand}
candidate_object_types:
  - {name: stock_movement, tasks: [Morning stock check], why: needs the ledger history}
open_questions:
  - Which warehouse counts online for the showroom?
---
# Role card: ops (p-klara)

| Task | Cadence | Starts when | Inputs | Outputs | Decisions (who approves) | Hours/week |
| --- | --- | --- | --- | --- | --- | --- |
| Morning stock check | daily | first thing, before orders ship | WooCommerce stock, ATUM ledger | SKUs to recount | which SKUs first (no approval) | 3 |

**Waiting on others:** supplier delivery dates for open purchase orders.

**One thing every morning:** a list of products whose stock is wrong, with the warehouse.

**Files mentioned (for the data amnesty):** stock corrections sheet on the shared drive.
````

Use `example: false` on real cards and `interviewed_on: null` only if the date is unknown.

If the person already has a card from a human-led interview, start from it and keep its
`handoffs`, `decides_alone`, `escalates`, `to_agree` and each task's `done_when` and
`baseline_minutes` exactly as they are: one card per person.
