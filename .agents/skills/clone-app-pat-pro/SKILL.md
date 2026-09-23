---
name: clone-app-pat-pro
description: Recreate a web application's UI from a reachable URL using measured DOM/CSS extraction and computed-style QA instead of screenshot guessing. Use for authorized site/UI replication, design-system extraction, or fidelity audits where browser automation is available.
---

# Clone App — Pat Pro for Codex

This is the Codex adapter for the original Claude-oriented workflow in this
repository. Preserve the original methodology and artifacts; replace only the
runtime/tool assumptions.

## Canonical method

Before starting, read these repository-root files:

- `../../../references/00-contract.md` — canonical artifact contract and gate.
- The stage reference needed for the current stage under `../../../references/`.
- `../../../scripts/assert-styles.mjs` and `../../../scripts/partition_bugs.py`
  when the corresponding QA/fix stage is reached.

Where this adapter and the original references differ only on Claude-specific
tool names or orchestration mechanics, this adapter controls the tool mapping.
The original contract continues to control artifact names, evidence rules,
stage outputs, and the convergence gate.

## Required browser capability

Exact-mode execution requires a browser surface that can do all of the
following against the target and the local clone:

1. navigate to a URL;
2. inspect/read the DOM;
3. execute JavaScript in the page so `getComputedStyle`, CSSOM and
   `getBoundingClientRect()` can be measured;
4. click, hover, focus, type, and open interaction-revealed states;
5. set or emulate the required viewport sizes; and
6. capture screenshots for visual reference.

Use the browser/computer capability available in the current Codex environment.
If a browser-control tool is not available but the target is public and the
workspace permits it, Playwright from the shell is an acceptable adapter.
Do not invent a tool name.

If no available browser surface can execute page JavaScript and exercise the
target UI, stop and report that exact/pixel-fidelity mode is blocked. Do not
replace measured extraction with screenshot guessing while claiming the same
confidence.

For authenticated sites, use only an already-authorized browser/session that the
user has explicitly made available. Never request, store, export, or commit
passwords, MFA values, cookies, local-storage tokens, or session credentials.

## Tool mapping

Translate Claude-specific instructions in the original references as follows:

- `mcp__claude-in-chrome__navigate` → available browser navigation.
- `javascript_tool` → browser page-JavaScript/evaluate capability.
- `read_page` / `find` → DOM/page inspection capability.
- `computer` click/hover/focus/screenshot → browser/computer interaction.
- `resize_window` → browser viewport/emulation control.
- Claude Task sub-agents → Codex sub-agents/parallel workers when the runtime
  supports them; otherwise execute the same disjoint tasks sequentially.
- Bash/Python/Node helper commands → shell execution in the checked-out repo.

The evidence hierarchy remains unchanged: authored CSS/CSSOM and measured
computed styles outrank screenshots. Screenshots are visual references unless a
separate reproducible image-diff path is actually available.

## Workflow

Run the original stages in order:

Recon → Extraction → Design Spec → Architecture → Build Foundation → Build
Pages → QA/Fix convergence loop → Polish → optional extension.

Preserve the original stop-and-check-in gate after each stage unless the user
explicitly asks for an autonomous run. If autonomous execution is requested,
still persist every required artifact and do not weaken the pass/fail gate.

### Recon

Exercise every reachable route/state, not one screenshot. Record sidebar items,
tabs, filters, menus, dialogs, panels, editor/focus states, hover states and the
three canonical viewports. Build the interaction map from observed UI only.

### Extraction

Measure values from the live DOM/CSS. Capture computed styles, authored rules,
pseudo-elements where observable, layout geometry, CSS variables, responsive
breakpoints, typography metadata, gradients, shadows and interaction-state
deltas. Record `null + reason` for values that cannot be measured.

Do not collect secrets or authenticated storage while inspecting the page.

### Design and build

Synthesize the measured values into `DESIGN.md` and
`assertions.json`, then build from those tokens. Reuse assets only when the
user is entitled to do so; otherwise preserve structure/fidelity with an
authorized replacement rather than silently copying restricted material.

### QA

For every asserted selector and required viewport, read the clone's actual
computed styles. Feed the measured JSON into
`../../../scripts/assert-styles.mjs`.

A pass requires:

- zero required style-assertion failures; and
- the build command exits successfully.

Do not claim a pixel-perfect or exact match merely because a screenshot looks
similar.

### Fix loop

Partition bugs by disjoint file ownership with
`../../../scripts/partition_bugs.py` when parallel workers are available.
After each fix, re-measure the affected selectors. Keep a change only if the
measured assertion improves or passes. Keep the build green.

## Safety and scope

Use this workflow only for sites the user is authorized to inspect/recreate and
within applicable terms, licences and access controls. Do not bypass paywalls,
authentication, anti-bot controls, or technical access restrictions.

Do not expose target-site secrets or private user data in clone artifacts,
logs, screenshots, design files, commits, or pull requests.

## Completion standard

Return one of the contract's honest terminal states. If exact measurement was
blocked, say what capability or page state was unavailable. Never downgrade the
method silently and still call the result exact.
