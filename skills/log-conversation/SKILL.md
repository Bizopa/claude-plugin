---
name: log-conversation
description: Log a call, meeting, site visit, WhatsApp chat or email in Bizopa CRM from the user's notes, a pasted transcript or an email — find the right customer, record what happened the way the workspace tracks it, update the deal where the conversation changed something, and offer a reminder for the next step. Use when the user says "log this call", "I just met Dr Tan", "add this to Bizopa", "update the deal after this meeting", pastes meeting notes or a transcript, or asks to record an email thread in the CRM.
---

# Log a conversation in Bizopa

One message from the user should leave the customer's record showing what happened, the deal up
to date, and the next step impossible to forget. Ask when something is unclear — never guess who
it was with.

## 1. Read what happened

Pull out of the notes, transcript or email:

- **Who** — the person and their company.
- **When** — today unless they say otherwise. Workspace time is `workspace.now` from `whoami`.
- **What kind** — call, meeting, site visit, email, WhatsApp.
- **What was said and agreed** — facts and commitments.
- **Which deal or job** it was about, and anything that **changed**: stage, amount, close date.
- **The next step**, and when.

If the source is an email or a calendar event in another connected app, read it there first.
Never log something you have not seen.

## 2. Find the right records

- `search` for the person and the company. Check each result's `subtitle` (the company it belongs
  to): several people or deals can share a name.
- One clear match: use it. Several: ask which one, naming each with its subtitle. None: ask
  whether to add them — then `describe-object` and `create-record`, linking the person to their
  company.
- For the deal or job: once you have the customer, `list-records` on the deals table with a
  `linked_to` filter on the customer (the `filter_as` name from `describe-object`) plus the deal
  name. Don't pick a deal from a title-only search — the same title can exist at other customers.

## 3. Record it the way this workspace does

`list-objects` and look for a table meant for conversations — Activities, Visits, Meetings, Calls.

- **There is one:** `describe-object` it, then `create-record` with the kind (use the choice's
  `value`, e.g. `call`, `meeting`, `site_visit`), the date and a short description. Pass `links` in
  the same call to the contact, the company and the deal, using the `relationships` from
  `describe-object`. If it links only to contacts, link the contact: its `reaches` shows the
  record reaches the company through them.
- **There isn't:** `add-note` on the deal (or on the contact when there is no deal).

Write it the way a colleague would want to read it later: two to six lines covering the date and
kind, who was there, what was discussed and what was agreed. Summarise; don't paste the
transcript. Leave out small talk, and anything personal or sensitive that doesn't belong in a
shared CRM (health details, private remarks), unless the user asks for it.

## 4. Update the deal only where the conversation says so

If something changed — the stage, the amount, the expected close date — `describe-object` the
table for the exact field names, the choice values and `editable_fields`. Then show the change
before making it:

> Stage: Proposal → Negotiation · Amount: RM 12,000 → RM 15,000

Apply it with `update-record` once they confirm. Don't read a stage change into a mood — "sounded
keen" is not Won. A won or paid record may be locked; pass the reason on plainly.

## 5. Offer the next step

When there is a follow-up ("send the quote Friday", "call back next week"), offer it: "Want a
reminder on Friday?" On a yes, `set-reminder` on the deal (or the contact) with that
day and a few words on what to do. Work the day out from `workspace.now`, and say the date back.
The reminder is theirs alone; a reminder for a teammate is set from the bell on the record page.

## 6. Confirm in two lines

What you logged, what changed, and when the reminder comes — with links to the records
(`<workspace url>/crm/objects/<table>/<id>`).

When one message covers several conversations, log each one the same way, then give one summary.
This flow never sends email and never deletes anything.
