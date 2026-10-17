# Changelog

Each release of this pack names the BFB Cookie Consent version it was checked against (`verifiedUpTo` in
`skills/bfbcc-update/references/index.json`). Skills and plugin are released together; a pack never describes a
plugin that has not shipped.

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
