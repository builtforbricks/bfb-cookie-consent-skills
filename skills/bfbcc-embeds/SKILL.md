---
name: bfbcc-embeds
description: "Use when adding or fixing a YouTube video or Google Map on a site running BFB Cookie Consent, or when the scan reports YouTube or Google Maps loading before consent: the bfbcc-youtube and bfbcc-google-map elements, their settings and placeholder, and why an ordinary embed keeps loading."
---

# BFB Cookie Consent: YouTube and Google Map embeds

Read `bfbcc-start-here` first. An ordinary embed (an iframe, Bricks' own Video or Map element) loads the provider at
once, before any consent. The plugin's two elements show a local placeholder instead and load the provider only after
the visitor allows the embed's purpose. Replace ordinary embeds with them; never put an ordinary iframe behind the
placeholder. Where an embed can't be replaced (a map another plugin draws, or Bricks' Map element fed by each post's
address), the owner holds it back instead: for Google Maps, the **Google Maps** switch under Services → Addresses to
hold back (`bfbcc-scan-findings`). While Google Maps waits, its placeholder also shows in the map boxes a script draws
into (WP Grid Builder's map facet, Bricks' Map element with an API key, `.acf-map`). For any other box, the element
needs the attribute `data-bfbcc-placeholder` set to `google-maps` (or a held address, as entered); in Bricks that is
Style > Attributes, an edit the owner approves.

The placeholder's look is set in Bricks: both elements have Placeholder, Placeholder text and Placeholder button style
groups (and "Remove the purple glow", "Hide the icon"). An owner who wants a placeholder of their own builds any block
with a Consent Action set to Open preferences (or `allow` with the category it waits for) inside and gives it `data-bfbcc-placeholder-for="google-maps"` (or a held
address): it shows only while the map waits and replaces the plugin's placeholders. A plain banner makes every
placeholder plain too.

## `bfbcc-youtube`

| Setting | Value |
| --- | --- |
| `video` | A video ID, or a watch, share, short or embed URL. Loads from `youtube-nocookie.com` after consent |
| `consent_category` | `preferences`, `analytics`, **`marketing`** (default) |
| `title` | The iframe's accessible title: "YouTube video" |
| `message`, `button` | The placeholder's text and its cookie choices button label ("Review cookie choices") |
| `load`, `hide_load` | The Load button's label ("Load video"), and `hide_load` switched on to show only the cookie choices button |
| `disclosure_provider`, `disclosure_description`, `disclosure_policy_url`, `disclosure_policy_label` | What the Consent Services list says about it |
| `privacy` | The owner's privacy classification. Leave it as it is (see below) |

## `bfbcc-google-map`

| Setting | Value |
| --- | --- |
| `embed_url` | Only the URL inside the iframe's `src` from Google Maps Share > Embed a map (`https://www.google.com/maps/embed?pb=…`, no API key needed), or a Maps Embed API URL with a key the owner restricts with Google |
| `consent_category` | **`preferences`** (default), `analytics`, `marketing` |
| `title`, `message`, `button`, `load` ("Load map"), `hide_load`, `disclosure_*`, `privacy` | As for YouTube |

Write `consent_category` explicitly: defaults are the builder panel's and raw JSON stores nothing for them.

## How it behaves

The placeholder has two buttons. Load allows the embed's `consent_category`, keeps the visitor's other choices, saves that and loads the embed in place; because choices are per category it allows everything in that category, so never describe it as consent to this one embed. Review cookie choices opens the visitor's choices and grants nothing. Held addresses' placeholders have the same pair (Load map for Google Maps). When the visitor allowed the
purpose but opted out of sale or sharing, the placeholder says the opt-out is holding the embed back: that is what
`privacy` decides, and it is the owner's call, so never change it. Withdrawing consent removes managed embeds again.
Adding or editing an embed on a page does not change the banner, so visitors are not asked again; the embed's
provider still belongs in the cookie list (`bfbcc-cookie-list`), which does.
