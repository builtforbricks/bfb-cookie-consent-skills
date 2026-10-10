---
name: bfbcc-setup
description: "Use when the owner asks to set up, check, audit or finish cookie consent on a site running BFB Cookie Consent, or asks what loads before consent: the plugin's five setup steps run through the bfb-cookie-consent/* abilities, a read-only check by default, and every change shown to the owner before it is made."
---

# BFB Cookie Consent: set up or check a site

Read `bfbcc-start-here` first. This flow follows the plugin's own five setup steps (Cookie Consent > Overview):
**See what your site loads, Choose your banner, Make them wait for permission, Tell visitors what you use, Switch on
and check.** It needs the `bfb-cookie-consent/*` abilities; if they are missing, the owner has not switched on
Overview > AI agents.

Two modes. **Check** changes nothing and is the default when the owner's request is unclear. **Set up** writes,
and the owner confirms each change first.

## Check (read only)

1. `get-status`. Report the plugin version, whether the banner is on, the template (valid, or its `problem`), the
   policy link, and which setup steps are done.
2. If no scan has run, or the owner changed things since, offer `run-scan`. It only reads the site's pages and changes
   nothing visitors see; it takes up to 20 seconds and may stop early on a slow host (run it again to continue).
3. `get-scan-findings`. Summarise by bucket, in the owner's words:
   - **Not gated, recognised**: loads before consent, and the library names it. The ones that matter most.
   - **Not gated, unrecognised**: loads before consent; identify it (`lookup-service`, the vendor's site).
   - **Consent platforms**: a second consent tool on the site; keep one.
   - **Infrastructure**: CDNs and hosting that carry files; usually nothing to hold back.
   - **Gated**: already waits for permission.
   For each not-gated item, say where it is probably installed (`bfbcc-scan-findings`) and what to do.
4. `get-services` and `get-cookie-list`. Look for gaps: a service in use with no entries in the list (does the
   library carry them? `descriptions_not_in_list` in the findings, or `lookup-service`), entries an agent wrote that
   nobody has checked (`written_by_agent_unchecked`).
5. Report a short list: what is done; what loads without permission; what the cookie list lacks; the open steps and
   who does each. Change nothing.

## Set up (each change shown to the owner first)

Agree the changes as one batch: changes to services, the cookie list and the policy link ask every visitor to choose
again once the banner is on.

1. **See what your site loads.** `run-scan`, then `get-scan-findings`.
2. **Choose your banner.** If `get-status` shows no valid template, offer `create-starter-banner`: a working banner
   with every required part, selected and still switched off. To restyle it or build the owner's own design, use
   `bfbcc-banner`. Never switch the banner on.
3. **Make them wait for permission.** For each not-gated service:
   - Google Analytics 4, Google Ads, Tag Manager, Clarity: the copy installed elsewhere must go first (find it with
     `bfbcc-scan-findings`; the owner removes it or approves your edit of a Bricks template). Then `set-preset` with
     the id the finding's `examples` show (`gtag/js?id=G-…`, `gtm.js?id=GTM-…`, `AW-…`, `clarity.ms/tag/<id>`). Tag
     Manager cannot sit beside the direct presets: choose one route with the owner.
   - Any other script: the owner registers it as a custom script on the Services tab (agents cannot), or uses the
     tool's own consent support. An ordinary YouTube or Google Maps embed: replace it with the plugin's element
     (`bfbcc-embeds`).
   - A second consent platform: the owner keeps one.
   Run the scan again afterwards: what is still not gated is outside the plugin's control.
4. **Tell visitors what you use.** `set-policy-url` with the address the owner gives you; never guess one. If the site
   has no cookie policy yet, offer to draft one (`bfbcc-cookie-policy`) for a lawyer to review. Then the
   cookie list (`bfbcc-cookie-list`): `add-library-entries` for every service whose library key has descriptions
   not yet in the list; for the rest, entries written from the vendor's own documentation with `save-cookie-entry`.
   The owner then ticks your entries as checked on the Inventory tab and confirms the step on Overview.
5. **Switch on and check.** Only the owner switches the banner on (Settings) and purges page caches. Then they test,
   in a private window: the banner appears first; **Reject**, then reload: the banner stays away and analytics shows
   no new visit; in a new private window, **Accept all**: the visit appears; **Preferences** (or the site's cookie
   settings link) reopens the choices. Then `run-scan` once more with the banner on.

## Finish

List what you changed and what each write returned (`visitors_asked_again`), and what is left for the owner: entries
to check, steps to confirm, the banner to switch on, the private-window test. Never call the result compliant;
describe it.
