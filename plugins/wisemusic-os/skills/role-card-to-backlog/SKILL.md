---
name: role-card-to-backlog
description: >-
  Use when the role cards from the onboarding interviews need to become a backlog of candidate
  skills, rules, actions and ontology changes, written as a pull-request description. Triggers
  include "turn the role cards into a backlog", "what should we build first", "first fifteen
  skills", "agenda for the ontology session", "backlog z karet rolí", "co postavit jako první".
  Dedupes candidates, counts the roles that need each one, checks what already exists, and keeps
  only items that a named person needs for a named decision.
---

# Role cards to backlog

**Owner:** the system owner. **Used by:** the system owner, area champions, whoever runs
onboarding.

1. **Collect the cards.** Either the person pastes them, or in Claude Code run
   `companyos-kit backlog instances/[company]`, which writes `discovery/backlog.md`, and read
   that file together with the cards in `discovery/role-cards/`. Skip cards marked
   `example: true`. List any person in `discovery/people.yaml` with no card yet.
2. **See what already exists.** Call `describe` for object types, properties, links, actions
   and metrics. In Claude Code also list the folders `skills/` and `instances/[company]/skills/`.
3. **Dedupe.** Merge candidates that mean the same thing (same steps, same check, same change)
   under one name. For each, count the distinct roles and people that need it and list the
   tasks it came from, with their `person_ref`.
4. **Start from a decision.** Each item must name a person (`person_ref` and role) and the
   decision it improves, taken from the cards' `decisions`. An item with no person or no
   decision goes to open questions, not to the backlog.
5. **Rank.** More roles first, then more hours per week in the source tasks, then items that
   serve the company's first slice. The top fifteen skills are the first fifteen. Add one
   `start-here-[role]` skill per role listing that role's five most-used skills.
6. **Propose ontology changes** only where a kept item needs them: an object type, property
   or link, each with a one-line reason. Keep ontology v0 at about a dozen object types.
7. **Write the pull-request description** in the format below. Show it to the person and
   adjust before anyone opens the pull request.

**The answer contains:** a three-line summary (cards read, items kept, items moved to open
questions), then the pull-request description as one Markdown code block.

**Never:** add an object type, rule, action or skill that no named person needs for a named
decision.

## Pull-request description format

Kinds are `skill`, `rule`, `action`, `metric`, `object type`, `property` or `link`. Proposed
files: skills in `instances/[company]/skills/[area]/[name]/SKILL.md` (company-wide skills in
`skills/[name]/SKILL.md`), rules in `rules.yaml`, actions in `actions.yaml`, metrics in
`metrics.yaml`, object types, properties and links in `ontology.yaml`.

````markdown
# Backlog from role cards ([company], [date])

## Why
[N] role cards from [roles]. These items repeat across roles or remove the biggest pains.
Each one names the person and the decision it improves.

## Skills
| Candidate | Kind | Roles needing it | From tasks | Already exists? | Proposed file |
| --- | --- | --- | --- | --- | --- |
| morning-stock-check | skill | ops, owner | Morning stock check (p-klara) | no | instances/[company]/skills/ops/morning-stock-check/SKILL.md |

## Rules
| Candidate | Kind | Roles needing it | From tasks | Already exists? | Proposed file |
| --- | --- | --- | --- | --- | --- |

## Actions
| Candidate | Kind | Roles needing it | From tasks | Already exists? | Proposed file |
| --- | --- | --- | --- | --- | --- |

## Decisions served
| Candidate | Person | Decision it improves |
| --- | --- | --- |
| morning-stock-check | p-klara (ops) | which SKUs to recount first |

## Ontology changes
- Add object type stock_movement (key: ledger id): p-klara needs the ledger history to decide which SKUs to recount.

## Deliberately not added
- [candidate]: [reason, e.g. one person, no decision named; already covered by an existing action; a skill is enough]

## Open questions
- [question, with the person_ref who raised it]

## Review checklist
- [ ] Every item names a person and the decision it improves
- [ ] Every new rule has fixtures that must and must not fire, and a backtest over history before it is switched on
- [ ] Every new action names proposer roles and approver roles, a preview, one writeback and one emitted event
- [ ] Restricted properties keep restricted_to (for example purchase prices and invoice amounts)
- [ ] Ontology v0 stays at about a dozen object types
- [ ] No personal data from the cards beyond person_ref
- [ ] companyos-kit validate passes on the instance
````
