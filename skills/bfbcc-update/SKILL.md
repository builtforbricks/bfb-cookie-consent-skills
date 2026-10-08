---
name: bfbcc-update
description: "Use when the user asks to check for or install BFB Cookie Consent skills updates, or when the plugin on the site seems newer than these skills describe. Compares the pack's verifiedUpTo with the plugin version on the site and, only on request, moves the checkout to the latest release."
allowed-tools: Bash, Read
---

# BFB Cookie Consent: check for skills updates

Prerequisite: the skills were installed from `https://github.com/builtforbricks/bfb-cookie-consent-skills` (a git
checkout, by default at `~/.bfb-cookie-consent/skills/bfb-cookie-consent-skills`, with each skill folder symlinked into
the client's skills directory).

## What it does

Says whether this pack describes the plugin on the connected site and, when asked, updates the pack. The plugin and
the pack are released together, so a mismatch means one of them moved and the other did not.

## Steps

1. **The pack's version.** Read `verifiedUpTo` in `references/index.json` beside this file. Ignore `version` (the
   pack's own number) for this comparison.
2. **The site's version.** Call `bfb-cookie-consent/get-status` and read `plugin_version`. Without the plugin's
   abilities (the owner has not switched them on), call `bricks/get-system-information` and read the `version` of the
   `plugins` entry named "BFB Cookie Consent". With no site connection, say one is needed to compare, and offer the
   pack-side check alone (step 4).
3. **Compare as versions.** Major, minor, patch left to right; a pre-release suffix (`-beta.2`) sorts below the
   release.
   - Equal: current; say so.
   - Site newer: the pack is behind and may not know a new ability or setting; recommend the update and wait.
   - Site older: the pack is ahead; an ability it names may be missing on the site.
4. **The latest release**, changing nothing: `scripts/bfbcc-skills-upgrade --check` from the repository root prints
   `BFBCC_SKILLS_INSTALLED`, `BFBCC_SKILLS_LATEST` and either `BFBCC_SKILLS_ALREADY_CURRENT` or
   `BFBCC_SKILLS_UPDATE_AVAILABLE <old> <new>`.

## Updating, only when the user asks

- `scripts/bfbcc-skills-upgrade` moves the checkout to the latest release tag (prints `BFBCC_SKILLS_UPDATED <old> <new>
  <tag>`), stashing local changes first and saying so. `scripts/bfbcc-skills-upgrade <tag>` moves to a named tag.
- If the checkout does not exist, clone it as the README says, then link the skills.
- The symlinks keep pointing at the same folders. **Start a new chat or session** afterwards: most clients load
  skills once, at the start.
