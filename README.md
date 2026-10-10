# BFB Cookie Consent skills

Agent skills for [BFB Cookie Consent](https://builtforbricks.com/cookie-consent/), the consent banner plugin for
Bricks Builder by Built for Bricks: how to set up or check consent on a site, build a banner that works, read the scan,
and write the cookie list. Checked against the plugin before every release.

**Status: complete, awaiting its first release.** The first release goes out with BFB Cookie Consent 1.0.0-beta.2, the
version it describes (`verifiedUpTo` in `skills/bfbcc-update/references/index.json`).

## What a skill is

A folder with a `SKILL.md`: a short front matter (`name`, `description`) and Markdown an AI client loads when the task
matches. It does not talk to the site; the connection does. Bricks 2.4 or later connects a client to the site through
the WordPress MCP Adapter, set up under **Bricks > AI**, and the plugin adds its own abilities once the site's owner
switches on **Cookie Consent > Overview > AI agents**. The skills tell the client what the abilities cannot: the parts
a banner needs or every service stays off, what asks visitors to choose again, where a tracker is usually installed,
how to write a cookie entry from the vendor's own documentation, and what never to touch.

## Requirements

- BFB Cookie Consent 1.0.0-beta.2 or later, on WordPress 6.9 or later for its abilities.
- Bricks 2.4 or later with its abilities enabled, for a client that works on the site.
- A client that loads skills: Claude Code, Codex, Cursor, GitHub Copilot, or any client that reads `SKILL.md` folders.

## Install

Copy the prompt from **Cookie Consent > Overview > AI agents** in WordPress into your client, or do it by hand.

**Claude Code, as a plugin** (updates with `/plugin marketplace update bfb-cookie-consent-skills`):

```
/plugin marketplace add builtforbricks/bfb-cookie-consent-skills
/plugin install bfb-cookie-consent@bfb-cookie-consent-skills
```

**Claude Code, Codex, Cursor and others, as a checkout** (one checkout, symlinked, so an upgrade moves every skill):

```sh
git clone https://github.com/builtforbricks/bfb-cookie-consent-skills.git ~/.bfb-cookie-consent/skills/bfb-cookie-consent-skills
~/.bfb-cookie-consent/skills/bfb-cookie-consent-skills/scripts/bfbcc-skills-upgrade   # pins the checkout to the latest release

# Pick the directory your client scans:
SKILLS_DIR="$HOME/.claude/skills"      # Claude Code, every project    (a project alone: .claude/skills)
# SKILLS_DIR="$HOME/.agents/skills"    # Codex and other agents         (Codex alone: ~/.codex/skills)
# SKILLS_DIR=".cursor/skills"          # Cursor, this project

mkdir -p "$SKILLS_DIR"
for skill in "$HOME"/.bfb-cookie-consent/skills/bfb-cookie-consent-skills/skills/bfbcc-*; do
  ln -sfn "$skill" "$SKILLS_DIR/$(basename "$skill")"
done
```

Then start a new chat and ask: *List the loaded skills whose names start with `bfbcc-`.*

## What is included

| Skill | Covers |
|---|---|
| `bfbcc-start-here` | Load first: how the plugin fits together, default denial, what asks visitors again, the tools, the workflow, never do |
| `bfbcc-setup` | Set up or check consent on a site, through the plugin's five setup steps: a read-only check by default, every change shown to the owner first |
| `bfbcc-banner` | The banner in Bricks: the structure without which every service stays off, each element's settings, Accept and Reject with equal weight, the starter banner as a checked example |
| `bfbcc-scan-findings` | The scan's buckets, where trackers are usually installed, remove at the source then register, what the scan cannot see |
| `bfbcc-cookie-list` | The cookie list: the library's checked descriptions first, otherwise the vendor's own documentation, exact names, durations never rounded down, the agent mark |
| `bfbcc-embeds` | The YouTube and Google Map elements and their placeholders |
| `bfbcc-cookie-policy` | Drafts the site's cookie policy from its real data, with the live cookie list embedded and placeholders for what no tool knows, saved as a draft page for a lawyer to review |
| `bfbcc-update` | Compares the pack with the plugin on the site; updates on request |

## What these skills never do

They never claim a site is compliant, and never present a policy as the plugin's or as checked. On its owner's request
a client drafts the cookie policy from the site's real data (`bfbcc-cookie-policy`); the draft is the owner's, and a
lawyer should review it before it is published. They never touch
consent records, opt-outs, custom scripts, the banner's on and off, or plugin data deletion: the plugin keeps those for
its owner, and its abilities do not offer them.

## How it is made, and why that matters

- Every element name, setting and ability a skill quotes is checked against the plugin before a release, and the
  starter banner in `skills/bfbcc-banner/references/starter-banner.json` is exported from the plugin itself.
  `verifiedUpTo` is the plugin version they were checked against, never typed.
- The plugin and the pack are released together, the same day. `scripts/bfbcc-skills-upgrade` pins a checkout to the
  latest release; `--check` only reports.

## Updating

Ask your client to "check for BFB Cookie Consent skills updates" (the `bfbcc-update` skill), or run
`~/.bfb-cookie-consent/skills/bfb-cookie-consent-skills/scripts/bfbcc-skills-upgrade`. Start a new chat afterwards:
most clients load skills once, at the start of a session.

## Licence

GPL-2.0-or-later, the plugin's. Built for Bricks, https://builtforbricks.com.
