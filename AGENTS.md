# Repository guidance

This fork preserves the original Claude-oriented Pat Pro skill and adds a
Codex-specific adapter without rewriting the upstream methodology.

For Codex work in this repository:

- Use `.agents/skills/clone-app-pat-pro/SKILL.md` for Codex execution.
- Treat the root `SKILL.md` and `references/` as the upstream Claude method.
- Do not replace Claude-specific instructions in the root files merely to make
  Codex work; keep the two runtime adapters separable.
- The root `references/00-contract.md` remains the artifact/gate authority
  unless an intentional, reviewed method revision changes it.
- Any claim of an exact/pixel-perfect clone requires measured browser evidence,
  not screenshot-only judgment.
- Never persist credentials, MFA values, cookies, session tokens, or other
  authenticated browser secrets.
- Do not add a licence on behalf of the upstream author. This fork currently
  reports no upstream licence; preserve attribution/history and treat reuse
  beyond the GitHub fork/personal workflow cautiously.
