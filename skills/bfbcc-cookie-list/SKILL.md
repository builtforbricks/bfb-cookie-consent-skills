---
name: bfbcc-cookie-list
description: "Use when adding, writing, checking, translating or removing entries in the BFB Cookie Consent cookie list (the Inventory tab; get-cookie-list, add-library-entries, save-cookie-entry, remove-cookie-entry), or when the owner asks what cookies a service sets: the library first, otherwise the vendor's own documentation, exact names, durations never rounded down, and the agent mark."
---

# BFB Cookie Consent: the cookie list

Read `bfbcc-start-here` first. The cookie list tells visitors what is stored on their device, by whom, for how long
and why. It describes; it registers and blocks nothing. Visitors see it through the Consent Inventory element (in the
preferences panel or on any page) or the `[bfbcc_inventory]` shortcode on the policy page.

## What is already there

`get-cookie-list` returns every entry. **Automatic** entries are the plugin's own (the visitor's consent choice and
privacy preference) and cannot be changed. The rest are the owner's, up to 100 by default.

## Library first

When `get-scan-findings` or `lookup-service` gives a `library_key` with descriptions, use `add-library-entries`. Those
rows were checked against the vendor's own documentation and dated; names already in the list are skipped. They are
starting points in English: some lifetimes are the site's own setting (a GA4 cookie's lifetime is configurable), so
say so to the owner.

## Writing an entry yourself

Only from the **vendor's own** cookie or storage documentation. For advertising and measurement vendors, the IAB TCF
Global Vendor List's device storage disclosure is the vendor's own statement too. Never copy another consent tool's
cookie database. Tell the owner which page you read.

| Field | Write |
| --- | --- |
| `service` | The name a visitor knows: "Google Analytics" |
| `provider` | The company: "Google Ireland Limited" for EU visitors where the vendor says so |
| `name` | Exactly as stored, a trailing `*` for a prefix: `_ga_*` |
| `type` | `cookie`, `localStorage`, `sessionStorage` or `other` |
| `category` | `necessary`, `preferences`, `analytics` or `marketing`: the purpose the service waits for on this site |
| `purpose` | What it does, in plain words, from the vendor's description |
| `duration` | The vendor's figure, **never rounded down**: "13 months", not "1 year"; "Session" for session storage |
| `policy_url` | The vendor's privacy page, https |
| `language` | Empty for every language; a locale (`ro_RO`) to show the entry in that language only |

To translate an entry, add another with the same `name` and the `language` set; the original stays for the other
languages. If the vendor publishes nothing you can read, say so and leave the entry out. Never invent a name, a
duration or a purpose.

## The agent mark

Every entry you save is marked **Added by an AI agent** on the Inventory tab until the owner ticks **Checked** and
saves. Visitors never see the mark, and checking does not ask them again. Ask the owner to check your entries against
the source you named; never tick it for them. `save-cookie-entry` replaces the entry with the same name and language
(it is then marked again). `remove-cookie-entry` removes only your unchecked entries; everything else the owner removes
on the Inventory tab.

Every change to the list asks visitors to choose again once the banner is on: write the entries as one batch.
