---
name: bfbcc-cookie-policy
description: "Use when the owner asks to write, draft, update or check the cookie policy (or the cookie section of the privacy policy) of a site running BFB Cookie Consent: build it from the site's real data through the bfb-cookie-consent/* abilities, embed the live cookie list, ask the owner for what no tool knows, save it as a draft page, and tell them to have a lawyer review it before it is published."
---

# BFB Cookie Consent: draft the cookie policy

Read `bfbcc-start-here` first. When the owner asks for a cookie policy, write one: a complete, readable draft built
from what the site really does, in the owner's voice. The text is theirs. You draft it, they decide what it says, and a
lawyer should review it before it goes live. Say so when you start and when you hand it over, and put the note at the
top of the draft.

## 1. Gather the facts (read only)

- `get-status`: `policy_url` (is there a policy to update?), `consent` (`choice_lasts_days`, `records_kept`,
  `records_retention_days`), whether the banner is on, the last scan.
- `get-services`: every registered service, its category, its script's host and its privacy classification.
- `get-cookie-list`: every entry, with its provider, purpose, duration, category and type. If entries an agent wrote
  are still unchecked (`written_by_agent_unchecked`), ask the owner to check them on the Inventory tab first, or
  mark them in the draft.
- `get-scan-findings`: what still loads before consent. A policy describes the site as it is. If services load without
  permission, tell the owner and offer to fix that first (`bfbcc-scan-findings`); never write that a service waits
  for consent unless it is registered (`get-services`) or shown through the plugin's own embed elements.
- `core/get-site-info`: the site's name and address.
- Ask the owner for what no tool knows: who runs the site (legal name and address), the contact for privacy questions,
  where the policy should live (its own page, or a section of the existing privacy policy), its language or
  languages, whether the site shows a "Do Not Sell or Share" link, and anything they want said about legal bases or
  transfers. If they do not know, leave a placeholder in square brackets, such as [Company legal name], and list
  every placeholder when you hand the draft over. Never invent a fact.

## 2. Write it

Plain words and short sections. Adapt this order to what the owner wants:

1. **What cookies and similar technologies are**, in a sentence or two. Include browser storage (localStorage): the
   plugin keeps the visitor's choice there.
2. **How this site uses them**, by category: what is necessary and always on (the consent choice itself, from the
   cookie list), then each optional category the site really uses (preferences, analytics, marketing) with its
   services and what they are for. Leave out categories with nothing in them.
3. **The cookie list.** Embed the live list rather than copying it: the Consent Inventory element (`bfbcc-inventory`)
   in Bricks, or the `[bfbcc_inventory]` shortcode. It updates itself when the list changes. If the owner also wants
   a table in the text, copy each entry exactly (names, providers, durations as written; never round a duration).
4. **Videos and maps**, if the site uses the plugin's YouTube or Google Map elements: they load only after the
   visitor allows them (`bfbcc-embeds`).
5. **Your choices.** Optional services stay off until the visitor allows them on the banner. How to change or
   withdraw a choice later (the site's Preferences or cookie settings link; ask the owner where it is). How long a
   choice lasts (`choice_lasts_days`), and that visitors are asked again when the site's services or cookie list
   change.
6. **Consent records**, only if `records_kept` is true: when a visitor accepts, rejects or saves a choice, the site
   records the decision, the allowed categories, the time it was received, a random record ID and the notice version,
   for `records_retention_days` days. No IP address, user agent, account, visitor identifier or page address is
   stored. If records are not kept, say nothing about them.
7. **Privacy opt-outs**, if the owner shows the "Do Not Sell or Share" link (`[bfbcc_privacy]`) or any service is
   classified as selling, sharing or targeting ads: visitors can opt out of the sale or sharing of their personal
   information and of targeted advertising, and a browser sending Global Privacy Control is treated as that opt-out.
8. **Who else receives data**: the providers named in the cookie list. Where it goes and under what safeguards, only
   as the owner states it; otherwise a placeholder for their lawyer.
9. **Legal basis**, if the owner wants it stated: write what they confirm (commonly consent for optional cookies, and
   the site's need to work for necessary ones), and flag it for their lawyer.
10. **Changes and contact**: the date of this version, that it changes when the site's tools change, and who to
    contact.

## 3. Hand it over

- Show the whole draft in the chat first.
- With the owner's yes, save it as a **draft** page they can review: Bricks' `bricks/create-post` creates a draft by
  default; put the Consent Inventory element where the list belongs. Never publish it.
- Once the owner (and their lawyer) have approved and published it, and only on their instruction, link it with
  `set-policy-url`. That asks every visitor to choose again once the banner is on, so batch it with other changes.

## Always

- The draft begins with: "Draft prepared with an AI assistant from this site's settings on [date]. Have it reviewed by
  a lawyer before you publish it." The owner removes the line when they are done.
- Tell the owner, in the chat, that you have not checked the text against any law and that a lawyer should review it.
- Never call the policy or the site compliant, "GDPR-ready", "approved" or "legally correct", and never say that BFB
  Cookie Consent or Built for Bricks wrote or checked it.
- When services or the cookie list change later, offer to update the policy. The embedded list updates itself; the
  words around it do not.
