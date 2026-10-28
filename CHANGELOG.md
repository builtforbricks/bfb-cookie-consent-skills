# Changelog

Each release of this pack names the BFB Cookie Consent version it was checked against (`verifiedUpTo` in
`skills/bfbcc-update/references/index.json`). Skills and plugin are released together; a pack never describes a
plugin that has not shipped.

## 0.3.6, 2026-10-28

Verified up to BFB Cookie Consent 1.2.6. No skill changes: 1.2.6 only changes when the plugin tells WP Consent API about
marketing.

## 0.3.5, 2026-10-27

Verified up to BFB Cookie Consent 1.2.5.

- `bfbcc-embeds` knows that the Placeholder text style also styles the Review cookie choices link.

## 0.3.4, 2026-10-26

Verified up to BFB Cookie Consent 1.2.4.

- `bfbcc-embeds` knows the placeholders' Load button (`load`, `hide_load`) and what it allows: one category, not one embed.
- `bfbcc-banner` knows the Consent Action's `allow` action, for placeholders an owner designs.

## 0.3.3, 2026-10-22

Verified up to BFB Cookie Consent 1.2.3.

- `bfbcc-banner` knows how the site's own links and WordPress menu items open the choices (the class bfbcc-open-preferences,
  `#bfbcc-preferences`).

## 0.3.2, 2026-10-21

Verified up to BFB Cookie Consent 1.2.2.

- `bfbcc-embeds` knows where the Google Maps placeholder shows for a map a script draws, and the
  `data-bfbcc-placeholder` attribute for any other box.
- `bfbcc-embeds` knows the placeholder style groups, the owner's own placeholder (`data-bfbcc-placeholder-for`) and
  that a plain banner makes placeholders plain.

## 0.3.1, 2026-10-21

Verified up to BFB Cookie Consent 1.2.1.

- `bfbcc-scan-findings` knows **Hold back** and the **Google Maps** switch: what is held back waits wherever it is
  installed. It knows what the button does for a Google Maps finding and for other addresses, that agents can't hold
  anything back, and what it doesn't cover.
- `bfbcc-start-here`, `bfbcc-setup` and `bfbcc-embeds` count held addresses among what waits for permission, and offer
  holding back for a map or widget that can't be replaced.

## 0.3.0, 2026-10-20

Verified up to BFB Cookie Consent 1.2.0.

- `bfbcc-banner` knows the Consent Banner's Style (styled or plain), the Consent Services element's policy link text,
  the new Consent Privacy Choices element, and that the banner must be a Section template.
- `bfbcc-scan-findings` knows the scan's Necessary group, and that only the owner marks a service as necessary.

## 0.2.1, 2026-10-17

Verified up to BFB Cookie Consent 1.1.1, whose dashboard wording is plainer. The skills name the dashboard as the
owner now sees it: the **Cookie list** tab (was Inventory) and the scan's **Known, not held back**, **Unknown, not held
back** and **Other consent tools** groups.

## 0.2.0, 2026-10-15

Verified up to BFB Cookie Consent 1.1.0.

- `bfbcc-setup`, `bfbcc-start-here` and `bfbcc-scan-findings` know the Meta, TikTok and Reddit pixel presets and where
  their ids appear, and that plugins supporting the WP Consent API follow the visitor's choice when that plugin is active.

## 0.1.2, never released

Verified up to BFB Cookie Consent 1.0.1, which shipped only inside 1.1.0. No skill changed: 1.0.1 adds the Tag Manager event `bfbcc_consent_update`,
which the developer guide documents.

## 0.1.1, 2026-10-11

Verified up to BFB Cookie Consent 1.0.0, the first public release. No skill changed: 1.0.0 is 1.0.0-beta.2's code
under its release version.

## 0.1.0, 2026-10-11

Verified up to BFB Cookie Consent 1.0.0-beta.2, the testers' build with the AI agent abilities.

- First pack: `bfbcc-start-here`, `bfbcc-setup`, `bfbcc-banner` with the starter banner exported from the plugin,
  `bfbcc-scan-findings`, `bfbcc-cookie-list`, `bfbcc-embeds`, `bfbcc-cookie-policy` and `bfbcc-update`.
