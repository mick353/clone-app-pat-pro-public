# Codex adapter

This fork keeps the original Claude skill intact and adds a repository-local
Codex skill at:

`.agents/skills/clone-app-pat-pro/SKILL.md`

OpenAI's current guidance uses `AGENTS.md` for repository policy and
`.agents/skills/*/SKILL.md` for repository-local reusable workflows.

The Codex adapter keeps the useful part of Pat Pro: measured DOM/CSS extraction,
a generated design system, and computed-style assertions as the QA gate. It
does not depend on Claude's Chrome-extension tool names. Instead, it maps the
workflow onto whatever browser/computer capability is actually available to the
Codex runtime, or Playwright for public/reachable targets when appropriate.

If the runtime cannot execute JavaScript in a browser and interact with the
target, the adapter fails closed rather than pretending a screenshot-only clone
has the same evidential quality.

## Use

From Codex in this repository, ask for the `clone-app-pat-pro` skill explicitly
or make a cloning request that matches its description.

Example:

`Use clone-app-pat-pro to recreate <authorized URL>. Preserve measured QA and stop after recon for approval.`

The original Claude installation path and root `SKILL.md` remain unchanged.
