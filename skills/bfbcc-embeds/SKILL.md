---
name: bfbcc-embeds
description: "Use when adding or fixing a YouTube video or Google Map on a site running BFB Cookie Consent, or when the scan reports YouTube or Google Maps loading before consent: the bfbcc-youtube and bfbcc-google-map elements, their settings and placeholder, and why an ordinary embed keeps loading."
---

# BFB Cookie Consent: YouTube and Google Map embeds

Read `bfbcc-start-here` first. An ordinary embed (an iframe, Bricks' own Video or Map element) loads the provider at
once, before any consent. The plugin's two elements show a local placeholder instead and load the provider only after
the visitor allows the embed's purpose. Replace ordinary embeds with them; never put an ordinary iframe behind the
placeholder.

## `bfbcc-youtube`

| Setting | Value |
| --- | --- |
| `video` | A video ID, or a watch, share, short or embed URL. Loads from `youtube-nocookie.com` after consent |
| `consent_category` | `preferences`, `analytics`, **`marketing`** (default) |
| `title` | The iframe's accessible title: "YouTube video" |
| `message`, `button` | The placeholder's text and its button label ("Review cookie choices") |
| `disclosure_provider`, `disclosure_description`, `disclosure_policy_url`, `disclosure_policy_label` | What the Consent Services list says about it |
| `privacy` | The owner's privacy classification. Leave it as it is (see below) |

## `bfbcc-google-map`

| Setting | Value |
| --- | --- |
| `embed_url` | Only the URL inside the iframe's `src` from Google Maps Share > Embed a map (`https://www.google.com/maps/embed?pb=…`, no API key needed), or a Maps Embed API URL with a key the owner restricts with Google |
| `consent_category` | **`preferences`** (default), `analytics`, `marketing` |
| `title`, `message`, `button`, `disclosure_*`, `privacy` | As for YouTube |

Write `consent_category` explicitly: defaults are the builder panel's and raw JSON stores nothing for them.

## How it behaves

The placeholder's button opens the visitor's choices; clicking it does not grant consent. When the visitor allowed the
purpose but opted out of sale or sharing, the placeholder says the opt-out is holding the embed back: that is what
`privacy` decides, and it is the owner's call, so never change it. Withdrawing consent removes managed embeds again.
Adding or editing an embed on a page does not change the banner, so visitors are not asked again; the embed's
provider still belongs in the cookie list (`bfbcc-cookie-list`), which does.
