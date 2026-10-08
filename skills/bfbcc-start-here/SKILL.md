---
name: bfbcc-start-here
description: "Load first in any session that sets up, checks, designs or edits BFB Cookie Consent, the consent banner plugin for Bricks Builder by Built for Bricks (the bfbcc-* elements and the bfb-cookie-consent/* abilities): how the plugin fits together, what asks visitors to choose again, the tools, what never to touch, and never claiming compliance."
---

# BFB Cookie Consent: start here

BFB Cookie Consent is a consent banner you design in Bricks. It holds back the services registered with it until a
visitor allows their purpose, scans the site's own pages for what loads before consent, and publishes a cookie list.
Load Bricks' own `bricks-start-here` first when it exists. Every other `bfbcc-*` skill assumes you have read this one.

## How it fits together

- **The banner** is one published Bricks template, selected under Cookie Consent > Settings, holding exactly one
  Consent Banner (`bfbcc-banner`) with its panels, actions and category switches. A banner placed on a page does not
  count; the selected template is the banner on every page. See `bfbcc-banner`.
- **Services** wait for permission: the four presets (Google Analytics 4, Google Ads, Google Tag Manager, Microsoft
  Clarity) and the owner's custom scripts, plus the plugin's own YouTube and Google Map elements. **Nothing else is
  held back.** A tag installed in the theme, another plugin, a Bricks code element or a tag manager keeps loading.
- **The scan** reads the site's pages as served and lists every third-party address they load that the plugin is not
  holding back. It finds; it never blocks. See `bfbcc-scan-findings`.
- **The cookie list** (the Inventory tab) tells visitors what is stored, by whom, for how long and why. It describes;
  it registers and blocks nothing. See `bfbcc-cookie-list`.
- **Purposes**: Necessary (always on), Preferences, Analytics, Marketing. Tag Manager waits for all three optional
  purposes, because a container can hold anything.
- **Default denial**: optional services stay off until the visitor allows their purpose. Closing the banner,
  scrolling, an old or malformed saved choice: none of them counts as consent.

## What asks visitors to choose again

A saved change to the banner template (its content too), the registered services, the cookie list, the policy link,
the consent lifetime or the language changes the consent revision, and once the banner is on every visitor is asked
again. So **batch changes**: agree the whole list with the owner, then make them together. Each write ability returns
`consent_revision_changed` and `visitors_asked_again`; say what they returned. Ticking an agent's entry as checked
does not ask visitors again.

## The tools

- **Bricks' abilities** (`bricks/*`, Bricks 2.4 or later) read and edit the banner template like any Bricks content.
- **The plugin's abilities** `bfb-cookie-consent/*`, only while the owner has switched on Overview > AI agents.
  Reading: `get-status` (call it first), `get-scan-findings`, `get-cookie-list`, `get-services`, `lookup-service`.
  Acting: `run-scan`, `add-library-entries`, `save-cookie-entry`, `remove-cookie-entry`, `set-preset`,
  `set-policy-url`, `create-starter-banner`. Administrators only.
- **When the abilities are missing**, the switch is off. Tell the owner where it is (Cookie Consent > Overview > AI
  agents) and stop. Do not work around it with other tools (Bricks' PHP execution, options, database writes).

## Workflow

1. `get-status`. Say the plugin version, whether the banner is on, whether the template is valid, which of the five
   setup steps are done.
2. Read before you write: the findings, the services, the cookie list.
3. **Show the owner every change before making it**, with what it will do to visitors. Then make it.
4. After changes, the owner tests in a private window (see `bfbcc-setup`, step 5). You cannot test consent for them.

## Never

- **Claim the site is compliant**, "GDPR-ready", "certified", or that the banner "blocks all tracking". Describe what
  the plugin does instead: it holds back the services registered with it.
- **Write legal text as the plugin's or these skills'.** If the owner asks you to draft a cookie or privacy policy,
  draft it from the plugin's data as their draft, say plainly that they must check it, and never call it compliant.
- Touch what the plugin keeps for the owner alone, by any route: consent records and their export, history, privacy
  opt-out settings and classifications, custom scripts, switching the banner on or off, "Delete all plugin data",
  capabilities, languages, A/B tests.
- Invent a cookie name, a duration or a purpose. If the vendor publishes nothing, say so.
- Tick an agent-written entry as checked, or confirm a setup step, on the owner's behalf. Those are theirs.
- Register a service while its copy installed elsewhere still loads: it then loads twice, once without permission.

## Honest limits to keep in mind

The scan reads pages as served, up to 50: it cannot see scripts added at runtime, tracking routed through the site's
own domain, or pages only signed-in visitors see. The bundled translations have not been reviewed by fluent speakers.
The plugin is not an IAB TCF or Google-certified consent platform. Consent records are what browsers report, not
proof. Check the pack against the plugin with `bfbcc-update`.
