---
name: bfbcc-scan-findings
description: "Use when reading or explaining the BFB Cookie Consent scan (run-scan, get-scan-findings, the Scan tab), when the owner asks why a tool loads before consent or where a tracker comes from: what each bucket means, how to find where a tag is installed, remove it there and then register it, and what the scan cannot see."
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
| `not_gated_recognised` | Loads before consent; the library names it | Remove it where it is installed, then register it (below) |
| `not_gated_unrecognised` | Loads before consent; unknown to the library | Identify it (`lookup-service`, the vendor's site), then as above |
| `consent_platforms` | Another consent tool on the site | Two consent tools fight; the owner keeps one |
| `infrastructure` | CDNs and hosting that carry files | Usually nothing to hold back; describe what they store, if anything. Google Fonts is not one: the library lists it under Preferences, because loading it from Google is a consent question in Germany (Bricks can host fonts locally) |
| `gated` | Already waits for permission | Nothing |

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
  plugin's element (`bfbcc-embeds`).

The presets take the id the examples show: `gtag/js?id=G-…` (Google Analytics 4), `AW-…` (Google Ads),
`gtm.js?id=GTM-…` (Tag Manager), `clarity.ms/tag/<project id>` (Clarity). Anything else is a custom script, which only
the owner adds (Services tab), or the tool's own consent support. The Services tab's **Check for duplicate tags** looks
for recognisable Google and Clarity tags on the home page.

## What the scan cannot see

Scripts added at runtime by other scripts, tracking routed through the site's own domain (a first-party proxy, server
side tagging), pages only signed-in visitors see, and anything beyond its 50 pages. So empty `not_gated_recognised` and
`not_gated_unrecognised` lists are good news about what was read, never a clean bill of health; say so when you report it.
