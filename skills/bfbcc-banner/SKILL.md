---
name: bfbcc-banner
description: "Use when building, restyling, rewording, translating or repairing the consent banner of BFB Cookie Consent in Bricks (bfbcc-banner, bfbcc-panel, bfbcc-action, bfbcc-category, bfbcc-services, bfbcc-inventory): the structure without which every service silently stays off, each element's settings, equal weight for Accept and Reject, keyboard and focus, and the test."
---

# BFB Cookie Consent: the banner

Read `bfbcc-start-here` first. The banner is ordinary Bricks content in a Bricks template (post type
`bricks_template`, published), selected under Cookie Consent > Settings. `get-status` returns its id, whether it is
valid, its `problem` if not, and `edit_url` for the builder. Edit it with Bricks' abilities like any template. A banner
placed on an individual page does nothing: the selected template is the banner everywhere.

## The structure that works (it fails silently)

Inside the selected template there must be **exactly one** `bfbcc-banner`, counting through Bricks components, and
inside that one banner:

| Part | Element and setting | How many |
| --- | --- | --- |
| The first view visitors see | `bfbcc-panel`, `view: "notice"` | exactly one |
| The detailed choices | `bfbcc-panel`, `view: "preferences"` | exactly one |
| Accept all | `bfbcc-action`, `action: "accept"` | at least one |
| Reject optional | `bfbcc-action`, `action: "reject"` | at least one |
| Open the choices | `bfbcc-action`, `action: "preferences"` | at least one |
| Save the choices | `bfbcc-action`, `action: "save"` | at least one |
| A switch per optional purpose | `bfbcc-category`, `category: "preferences"`, `"analytics"`, `"marketing"` | exactly one each |

If any of it is missing, duplicated or hidden, **every optional service stays off and the page shows nothing
wrong.** The dashboard catches a missing or second banner root; it cannot see a missing action inside it, so check the
tree yourself after every edit. A `necessary` category switch is optional and always on. Conditions, query loops and
custom CSS that hide a part count as missing on the published page: never hide one.

## The elements

| Element | Settings (stored value, default in bold) | Notes |
| --- | --- | --- |
| `bfbcc-banner` | `position`: **`left`**, `right`, `center` (bottom left, right, centre); `preview`: **`notice`**, `preferences`, `all` (which panel the builder shows; visitors are unaffected) | Nestable root. One per template |
| `bfbcc-panel` | `view`: **`notice`**, `preferences` | Nestable. Holds any Bricks content |
| `bfbcc-action` | `action`: `accept`, `reject`, **`preferences`**, `save`, `back`, `privacy`; `text`: the label | A button, except `privacy`, a link to the site's privacy-choices page ("Do Not Sell or Share My Personal Information"); `back` returns from preferences to the notice |
| `bfbcc-category` | `category`: `necessary`, `preferences`, **`analytics`**, `marketing`; `label`; `description` | A switch; Necessary is permanently on and disabled |
| `bfbcc-services` | none | Lists the registered services, the browser-preference entry and the policy link |
| `bfbcc-inventory` | `category`: **all**, or one purpose | The cookie list as a table; also on any page, or `[bfbcc_inventory]` |

Defaults are the builder panel's: raw JSON stores nothing for a default, so **always write `action`, `view` and
`category` explicitly**. Headings, text, layout blocks, images and classes are ordinary Bricks elements and settings.

## The verified pattern: the starter banner

`references/starter-banner.json` is the plugin's own starter, exported from the plugin and checked against it before
the pack is released: a notice panel (heading, text, Reject, Accept, Preferences) and a preferences panel (heading,
text, the four category switches, the services list, Save, Reject, Back). It is what `create-starter-banner` makes.
Start from it rather than from nothing; restyle it with ordinary Bricks settings.

A starter made before `1.0.0-beta.2` has 8-character element ids, and Bricks' abilities refuse to render or update it
(`bricks_invalid_element_id`); in the builder, right-click actions on its elements do nothing. Ask the owner before
saving it again with new 6-character ids: keep every element, setting, label, parent and order, and tell them that
custom CSS naming the old `#brxe-` ids needs the new ones.

## Design rules

- **Accept and Reject carry equal weight**: same size, same visual level, same step (both on the notice). A Reject
  hidden behind Preferences, greyed out or smaller is the pattern regulators reject.
- No optional switch is on before the visitor chooses; do not add settings or scripts that pre-tick them.
- Keep keyboard focus visible, and do not add `tabindex`, `role` or `aria-*` to the plugin's elements: they carry
  their own. Opening Preferences moves focus into the banner by itself.
- Plain words. No promises about compliance in the banner's text.
- Never put an iframe, a script or a tracking pixel inside the banner.

## After an edit

Any change to the template's content asks every visitor to choose again once the banner is on, so batch edits. The
Overview tab previews the saved banner (buttons inactive). Then the owner tests the published page in a private
window (`bfbcc-setup`, step 5). With Polylang, each language has its own translated, published template; a missing
translation keeps that language's services off.
