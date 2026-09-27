---
name: set-up-workspace
description: Tailor a Bizopa CRM workspace to how the user's business really works — a short interview about what they sell, who pays them and how a job moves along, then a plain-language plan of tables and fields to rename, add or switch off, built only after they agree. Use when someone is new to Bizopa, says the workspace doesn't fit their business, or asks to set up, customise or reorganise Bizopa ("set Bizopa up for my clinic", "I also need to track vehicles", "our steps are different", "add a field for…").
---

# Set up a Bizopa workspace

The person is usually a busy owner who has never set up a CRM. The goal is their own business,
in their own words, working in Bizopa within a few minutes — with nothing they have to learn first.

## 1. Look before you ask

1. `whoami` — note the workspace name, its `url`, and `can.manage_workspace`. Only admins can
   change tables and fields. If they are not an admin, still do the interview, then hand them a
   short written plan to pass to their admin instead of attempting the changes.
2. `list-objects`, then `describe-object` on the main tables (usually the people, the companies
   and the deals or jobs table).
3. A new workspace already starts from an industry template, so most of what they need is
   probably there under other names. Tailor it — rename, add the few missing pieces, switch off
   clutter. Never rebuild what exists, and never add a second table for something already tracked.

Tell them in a sentence or two what they already have ("You already have Customers, Deals that
move from New to Won, and Activities for calls and visits.").

## 2. Ask a few plain questions

At most five, one or two at a time, skipping anything the workspace or the conversation already
answers:

- What do you sell or do, and who pays you — companies, individuals, or both?
- From the first enquiry to getting paid, what are the steps? (These become the stages.)
- What do you note down about each customer or job that you'd hate to lose? (These become fields.)
- Is there anything else you keep track of — vehicles, properties, classes, contracts?
  (That may become its own table.)
- Who else will use it? (Inviting people happens in the app, under Settings → Members.)

Use their words for everything. Never say object, schema, field type, api name, entity or
association to them — say table, field, choice, stage, link.

## 3. Propose a plan, then wait for a yes

Keep it short, grouped by table, with no more than about eight new fields in the first pass:

> **Deals → call them "Jobs"**
> - Stages: Enquiry → Quote sent → Booked → Done → Paid (Lost stays, for jobs that fall through)
> - Add: Job address, Preferred date, Deposit paid (yes/no)
>
> **New table: Vehicles** — Plate number, Model, Next service date. Each vehicle belongs to one customer.
>
> **Switch off:** Campaign source, Lead score — you said you don't use them; they can come back any time.

Ask "Shall I set this up?" and change nothing until they agree. If they adjust the plan, show
the new version and confirm once more.

## 4. Build it

Work in this order and say briefly what you are doing as you go.

1. **Renames** — `update-object` for a table's name, `update-field` for a field's label. The
   internal name never changes, so nothing that points at it breaks.
2. **New tables** — `create-object` with a singular, lowercase name (`vehicle`,
   `service_visit`). It starts with one Name field.
3. **New fields** — `add-field`, choosing the type from what they said:

   | They describe | Type |
   |---|---|
   | a short piece of text, a code, a reference | `text` |
   | notes, a description | `long_text` |
   | an amount of money | `currency` |
   | a quantity or other number | `number` (or `percent`) |
   | a day / a day and time | `date` / `datetime` |
   | yes or no | `boolean` |
   | one choice from a list / several choices | `select` / `multiselect`, with `options` |
   | a phone number, email, website | `phone` / `email` / `url` |
   | an address | `address` |
   | files or photos | `attachment` |
   | a 1–5 star score | `rating` |
   | another record ("the customer this belongs to") | `link`, with `target` |

4. **Links between tables** — check `relationships` in `describe-object` first. "Each vehicle
   belongs to one customer" is `add-field` with type `link`, `target` the customer table and
   `multiple` false (or `create-relation` one_to_many). "Many people on many deals" is
   many_to_many.
5. **Stages** — change the choices of the EXISTING stage field with `update-field`. Send the full
   list, keep existing values exactly as they are, and keep each choice's `category` (open, won,
   lost) and `probability` as `describe-object` returned them. A new in-progress step gets
   category `open`. Never add a second stage field.
6. **Switch off what they don't use** — `update-field` with `is_active` false. The values are kept
   and the field can come back. Do not use `delete-field` in this flow.

Leave fields optional unless they ask for required. If a step is refused (not an admin, the table
is locked, a name is taken), pass the reason on in plain words and carry on with the rest.

## 5. Show it working

Offer to add one or two of their real customers or jobs now: "Tell me your latest customer and
I'll add them so you can see it." Use `describe-object`, then `create-record` with `links` to
connect the new record to the ones it belongs to.

## 6. Wrap up

- Three to six bullets on what changed, each table linked as `<workspace url>/crm/objects/<name>`.
- Point to the app for what this flow doesn't do: formulas and rollups (Settings → Objects → the
  table → Add field), automations (`<workspace url>/crm/settings/automations`), importing a
  spreadsheet (`<workspace url>/crm/objects/<name>/import`) and inviting people
  (`<workspace url>/crm/settings/members`).
