---
name: bfbcc-scan-findings
description: "Use when reading or explaining the BFB Cookie Consent scan (run-scan, get-scan-findings, the Scan tab), when the owner asks why a tool loads before consent or where a tracker comes from: what each bucket means, how to find where a tag is installed, remove it there and then register it, or hold back its address, and what the scan cannot see."
---

# BFB Cookie Consent: the scan and its findings

Read `bfbcc-start-here` first. `run-scan` reads the site's own pages as served (the home page, the sitemap's pages,
the WooCommerce cart, checkout, account and shop pages, the privacy policy page; up to 50) within one 20-second budget,
and stores a report. On a slow host it stops early (`stopped_early`); run it again and it continues where it stopped.
`read_nothing` means the host stops the site from requesting its own pages (Tools > Site Health says so too) or the
pages are too slow: an empty report then proves nothing.

## The buckets

Each finding is a third-party **address** with the **pages** it was seen on, **examples** of the URLs, the
library's **service** name and **category** when it knows the address, and a **library_key** when the plugin carries
storage descriptions for it.

| Bucket | Means | What to do |
| --- | --- | --- |
| `not_gated_recognised` | Loads before consent; the library names it | The owner holds back its address (**Hold back** on the Scan tab), or removes it where it is installed and registers it (below) |
| `not_gated_unrecognised` | Loads before consent; unknown to the library | Identify it (`lookup-service`, the vendor's site), then as above. **Hold back** files an unknown address as Marketing until the owner checks it |
| `consent_platforms` | Another consent tool on the site | Two consent tools fight; the owner keeps one |
| `infrastructure` | CDNs and hosting that carry files | Usually nothing to hold back; describe what they store, if anything. Google Fonts is not one: the library lists it under Preferences, because loading it from Google is a consent question in Germany (Bricks can host fonts locally) |
| `gated` | Already waits for permission: registered, held back by address, or a Consent element | Nothing |
| `necessary` | Strictly necessary, by the library (Cloudflare Turnstile) or the owner's marking | Nothing to hold back; it still belongs in the cookie list and privacy policy. Only the owner marks a service as necessary, on the Scan tab: never suggest it to get a step done |

## Registering does not stop a copy installed elsewhere

The plugin holds back only what is registered with it. A Google Analytics tag in the theme keeps loading even after
the GA4 preset is set: it then loads twice, once without permission. So the order is always **remove at the source,
then register, then scan again**. Where tags usually live:

- **Bricks**: Settings > Custom code (header and body scripts), a Code element in a template or page, a template
  or page's own custom code. Bricks' abilities can search templates and pages for the address; read, show the owner,
  and change only what they approve.
- **Another plugin**: Site Kit, MonsterInsights, PixelYourSite, header-and-footer script plugins, WooCommerce
  marketing extensions. Its own settings remove the tag; say which plugin, the owner switches it off there.
- **The theme or a child theme**: `functions.php` or a header file. The owner or their developer removes it.
- **A tag manager container** installed elsewhere: everything in it loads without the plugin knowing. Use the Tag
  Manager preset instead, with the plugin's consent template imported in the container (Services tab).
- **An ordinary embed**: a YouTube or Google Maps iframe, Bricks' own Video or Map element. Replace it with the
  plugin's element (`bfbcc-embeds`), or hold back its address (below) when it can't be replaced.

## Hold back an address

The other route, and the only one for a tool that can't be removed without losing it: a map from WP Grid Builder's
map facet, Bricks' Map element fed by each post's address, a widget another plugin adds. The owner presses **Hold
back** on the finding, or uses Services → Addresses to hold back. Everything from that address then waits until the
visitor allows its category, wherever it is installed, including when another script adds it later; iframes show a
placeholder.

- **Google Maps** has its own switch there, covering every address it loads from (`maps.googleapis.com`,
  `maps.google.com`, `google.com/maps`), whichever plugin or Bricks element shows the map; it waits for Preferences.
  **Hold back** on a Google Maps finding switches it on. A Google Maps address typed as its own entry is refused.
- **Any other address**: Hold back adds it under Other addresses, named and categorised from the library (an unknown
  one starts as Marketing). A shared host is narrowed to the service's path.
- **A plugin on the site itself** (plugin 1.2.7 and later): on the site's own host only one plugin's folder can be
  added, by the owner under Other addresses, such as `example.com/wp-content/plugins/plugin-name/`. It is for a plugin
  that tracks visitors from its own scripts without asking the WP Consent API (an affiliate plugin's visit tracker, for
  one). The scan doesn't list scripts from the site's own domain, so find the folder in the page source or the plugin's
  documentation, and name its cookies so they are cleared. Pages, uploads, themes, WordPress and this plugin's own
  folder are refused.

Agents can do neither: point the owner to the switch or the button. It does not hold back images, fonts or
stylesheets, and it is not automatic blocking: only Google Maps, when switched on, and the listed addresses wait.

The presets take the id the examples show: `gtag/js?id=G-…` (Google Analytics 4), `AW-…` (Google Ads),
`gtm.js?id=GTM-…` (Tag Manager), `clarity.ms/tag/<project id>` (Clarity), the digits in `fbq('init', …)` (Meta Pixel),
the `sdkid=` in `analytics.tiktok.com/i18n/pixel/events.js` (TikTok Pixel), the `a2_…` or `t2_…` in `rdt('init', …)`
(Reddit Pixel). Anything else is a custom script, which only
the owner adds (Services tab), or the tool's own consent support. The Services tab's **Check for duplicate tags** looks
for recognisable Google and Clarity tags on the home page.

## What the scan cannot see

Scripts added at runtime by other scripts, tracking routed through the site's own domain (a first-party proxy, server
side tagging), pages only signed-in visitors see, and anything beyond its 50 pages. So empty `not_gated_recognised` and
`not_gated_unrecognised` lists are good news about what was read, never a clean bill of health; say so when you report it.
