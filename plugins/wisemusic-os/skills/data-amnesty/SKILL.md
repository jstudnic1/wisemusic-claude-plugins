---
name: data-amnesty
description: >-
  Use when someone lists their private spreadsheets, notebooks and files for the data amnesty,
  or asks what should happen to a sheet they keep on the side. Triggers include "data amnesty",
  "my spreadsheets", "shadow data", "private Excel", "the sheet only I use", "datová amnestie",
  "moje tabulky", "soukromé soubory". Asks a few questions per file, proposes retire, govern or
  keep for each, without blame, and outputs rows for the company's data-amnesty list. Never
  needs the file's contents.
---

# Data amnesty

**Owner:** the system owner. **Used by:** every employee in the first week; process owners
whenever a new side sheet appears.

An amnesty: nobody is blamed for any file. The goal is to know where work data lives outside
the official systems, so it can move somewhere everyone can trust.

1. **Open with the promise:** "No blame for any file. I only need names and column headers,
   never the contents." Say it in the person's language.
2. **List every file first.** Spreadsheets, Google Sheets, exports on the desktop, notebooks,
   paper lists, email folders used as a to-do list. Probe once: "Anything you open every week
   that is not in a company system?"
3. **Ask about each file, one at a time:**
   1. What is it, in a few words?
   2. Where does it live (shared drive, laptop, email, paper)?
   3. What is it for: which task or decision?
   4. Which columns does it have? Header names only.
   5. Who reads it (roles)?
   6. How often is it updated, and by which role?
   7. Which columns hold personal data (customer names, emails, phones, addresses, IČO)?
4. **Optional, only if the company connector is connected:** call `describe` to see whether
   an object type or action already covers the file, for example a rental, a purchase order
   or a product's stock.
5. **Propose a fate** for each file with the definitions and the guide below. Explain the
   reason in one sentence. The person may disagree; record their view in the purpose or
   target. The system owner and the data owner decide later.
6. **Read the rows back** and let the person correct them.
7. **Output the rows** in both formats below: table rows and YAML entries, ready to paste into
   `discovery/data-amnesty.md`.

**The answer contains:** one short line per file with its proposed fate and reason, then the
Markdown table rows, then one fenced YAML block with the same files.

**Never:** ask for, open or copy the contents of a file; only its name, location and column
headers.

## Fates

| Fate | Means | Target |
| --- | --- | --- |
| retire | The data moves into a system or an action, and the file stops being updated. Example: the rentals spreadsheet moves to the rental_create, rental_extend and rental_return actions. | The action(s) or the system and object type that take over |
| govern | It stays a Google Sheet, with fixed columns and validation. Company OS reads it hourly, diffs it against the previous snapshot into events, and writes invalid rows to an errors tab for the owner. | The governed sheet and its owner role |
| keep | It stays as it is. Only with a reason and an owner. | The reason and the owner role |

## Guide

| If the file | Propose |
| --- | --- |
| Copies data a system already holds (stock, orders, prices) | retire, target: the system and object type |
| Records changes an action exists for, or will (rentals, stock corrections) | retire, target: the action(s) |
| Is shared and structured, but no system holds this data yet | govern |
| Is one person's working notes with no shared data and no personal data | keep, with reason and owner |
| Holds personal data in a private file | never keep; retire or govern, and flag it |

If a person pastes rows by mistake, ignore the values, keep only the headers, and say so.

## Output format

Table rows (the table in `discovery/data-amnesty.md` has these columns):

```markdown
| File | Owner role | Where | Purpose | Columns | Read by | Updated | Personal data columns | Fate | Target |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Rentals spreadsheet | sales | shared drive | who has which panel and until when | customer, panel, start, due, deposit, returned | sales, ops | per rental | customer | retire | rental_create, rental_extend and rental_return actions |
```

YAML entries (append under `files:` in the one fenced YAML block):

```yaml
files:
  - file: Rentals spreadsheet
    owner_role: sales
    purpose: who has which panel and until when
    columns: [customer, panel, start, due, deposit, returned]
    fate: retire                # retire | govern | keep
    target: rental_create, rental_extend and rental_return actions
```

For `keep`, `target` holds the reason and the owner role, for example "personal checklist, no
company data; owner: ops".
