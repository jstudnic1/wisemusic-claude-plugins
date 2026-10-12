---
name: propose-a-change
description: >-
  Use whenever someone wants to change something in a company system, such as setting stock
  after a count, moving an order to another status, recording a rental or its return, moving
  stock between warehouses or receiving a purchase order, and when they ask whether a change
  went through. Triggers include "change", "set stock", "update the order", "did it go through",
  "změň", "nastav sklad", "změň stav objednávky", "prošlo to?". Every change is a proposal that
  a person with an approver role approves.
---

# Propose a change

**Owner:** the system owner. **Used by:** everyone whose role may propose actions.

Nothing changes on a tool call alone. A change is proposed, a person approves it, the source
system is written first, and only then is the event recorded.

1. **Find the action.** Call `describe` and read the actions: what each does, who may propose
   it and who approves it. Pick the one that matches. If none does, say so and suggest adding
   it to the friction log; never work around it in another system.
2. **Resolve the object** with `search` and `get` (the SKU, order number or rental id) and
   read its current state, so the change makes sense against it.
3. **Fill the parameters exactly** as the action defines them. Ask for every missing value.
   The reason is the person's own words; never invent one. For a new action, take the
   parameters from `describe` and check them in the preview.
4. **Propose.** Call `propose_action` with the action name and its parameters. For example,
   setting a product's stock after a count needs the product id, the counted quantity and the
   reason. You get a request id, a preview and the status pending. If it is refused: "role
   required" means this person cannot propose it, so name the roles that can; a parameter
   error names the field to fix.
5. **Show the preview and explain what happens next:** a person with an approver role for
   this action approves or rejects it in the approval queue (approvals.[company domain]), one
   tap on the web or the phone. On approval the source system is written first; only if that
   succeeds is the event recorded.
6. **Check with `action_status`** using the request id when the person asks, or before
   saying anything about the result.
7. **Report the status in plain words** (table below). Only when it is executed, say it is
   done, and `get` the object to show the new state.

**The answer contains:** the preview, the request id, the current status in plain words, and
who can approve it.

**Never:** say a change is done before `action_status` shows executed.

## Statuses

| Status | Means | Tell the person |
| --- | --- | --- |
| pending | Waiting for an approver | Who can approve it, and that nothing has changed yet |
| executing | Approved; the source system is being written | Check again in a moment |
| executed | The source system accepted it and the event is recorded | It is done; show the new state |
| failed | The source system refused it; nothing changed | The error, the likely cause, and that it can be proposed again once fixed |
| rejected | The approver said no; nothing changed | Ask the approver why before proposing again |
