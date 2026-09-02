# Canonical task prompt: Nixvim upstream audit

This file is the authoritative task specification for the monthly Nixvim audit. The scheduled automation should read this file on every run rather than trying to embed the full task logic in the scheduler prompt.

## Target

Audit the user's current Nixvim configuration in `zaviro/nix-config` and decide whether it should be iterated.

## Required state reads

Before analysis:

1. Read `tasks/nixvim-upstream-audit/status.md`.
2. Read `tasks/nixvim-upstream-audit/history.jsonl`.
3. Inspect the current live `next` branch of `zaviro/nix-config`.
4. If an existing `cloud/nixvim-*` handoff candidate exists for the same intent, inspect it too; do not assume it is integrated.

## Standing upstreams checked every run

Always inspect current relevant changes in:

- `neovim/neovim`
- `nix-community/nixvim`
- `nvim-lua/kickstart.nvim`
- `LazyVim/LazyVim`

Focus on changes since the previous audit where practical, especially:

- Neovim release/news/default behavior
- native LSP, diagnostics, statusline, completion, Treesitter, comment and project-local configuration
- Nixvim breaking/deprecated modules, defaults, wrapper/nixpkgs behavior and plugin modules
- Kickstart's current minimum complete development baseline
- LazyVim's mature UX patterns, conflict handling and fallbacks

## Rotating mature Nixvim configurations

Use the current `nix-community/nixvim` official user-config list as the source of rotating repositories.

Each run choose 5–8 active repositories not present in the most recent audits in `history.jsonl`. Prefer a mixed sample:

- 1–2 minimalist configurations
- 1–2 larger mature configurations
- 1–2 LazyVim/distribution-inspired configurations
- 1–2 project-oriented/modular configurations

Before counting a rotating repository toward the 5–8 sample, validate that its current source URL resolves, the repository is not archived or disabled, and it still shows meaningful maintenance activity. Prefer repositories with meaningful pushes within roughly the last 12 months unless an older repository is intentionally used for historical comparison. Record missing, moved, archived, or materially stale official-list entries as skipped and replace them with another active sample; skipped entries do not count toward the 5–8 target.

Do not repeat a rotating repository merely because it is familiar. Revisit one only when it materially changed or a specific capability comparison requires it.

Record the exact repositories and audit date after every run.

## Capability matrix

Evaluate at least:

- Core options
- Autocmds
- Clipboard
- Indentation
- LSP
- Completion
- Syntax / Treesitter
- Diagnostics
- Formatting
- Lint
- Picker/search
- File management
- Code navigation
- Text objects
- Surround
- Commenting
- Buffers
- Windows
- Statusline
- VCS
- Terminal
- Session/project behavior
- Testing
- Debugging
- UI
- Health/recovery

Classify each relevant finding as one of:

`KEEP`, `ADD`, `REMOVE`, `REPLACE`, `DEFER`, `OMIT`.

## Acceptance standard

Preference order:

`Neovim native capability > small focused plugin > large plugin > copied distribution behavior`.

A change is material when at least one is true:

1. compatibility, breakage or deprecation requires it;
2. a Neovim native feature can replace an existing plugin/configuration cleanly;
3. it solves a clear high-frequency problem in the user's real TS/Nix/JJ/Yazi workflow;
4. there is strong cross-upstream convergence and the change improves the current baseline without duplicating an existing capability.

Actively look for removals and simplifications, not only additions.

Default to rejecting:

- single-source novelty;
- cosmetic-only additions without workflow value;
- capabilities already covered by the current stack;
- distribution-style plugin chains without a concrete need;
- Git-centric semantics that conflict with the user's JJ-first workflow;
- globally pinning project tools when the project environment should own them.

## Nixvim-specific rules

- Prefer Nixvim's own pinned/tested nixpkgs unless current upstream guidance materially changes.
- Do not set `nixpkgs.useGlobalPackages = true` without a concrete reason.
- Do not update `flake.lock` for a configuration/refactor-only change. Update it only when a dependency update is actually part of the accepted change.
- Keep project-owned tools such as Biome project-provided unless the user's repository policy changes.

## Change workflow

If no material improvement is warranted:

1. Do not modify `zaviro/nix-config`.
2. Update `status.md`.
3. Append one JSON object to `history.jsonl` with date, upstreams, rotating repos, findings and result=`no-change`.
4. Notify the user concisely.

If a material improvement is warranted:

1. Use the established `/rh` remote-handoff workflow for `zaviro/nix-config`.
2. Re-fetch the live `next` ref immediately before creating/updating the candidate.
3. If a same-purpose remote candidate exists and has not moved unexpectedly, replace/refine that candidate rather than stacking exploratory commits.
4. Keep the handoff to the smallest complete intent; no unrelated refactors.
5. Do not move `main` or `next` as part of producer-side handoff.
6. Do only cheap producer-side validation that is actually available; never claim atlas/Nix/Neovim runtime validation that was not run.
7. Ensure the final handoff commit contains the required Handoff metadata and produce the standard receipt.
8. Record candidate ref/OID, base ref/OID, rationale and unverified checks in this task's state files.
9. Notify the user with findings, changes and receipt.

## Progress storage

`zaviro/agent-task-progress` is the durable external memory for scheduled tasks. The scheduler prompt should remain compact and point to this file. Store task-specific durable details here when they are too large or stateful for the scheduler itself.

After every run:

- update `tasks/nixvim-upstream-audit/status.md` with current status, last result and next rotation guidance;
- append exactly one line to `tasks/nixvim-upstream-audit/history.jsonl`;
- include the exact audit date/timezone and repositories inspected.
