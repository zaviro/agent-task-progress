# Nixvim upstream audit

- Task ID: `nixvim-upstream-audit`
- Cadence: monthly
- Target config: `zaviro/nix-config`
- Canonical task specification: `tasks/nixvim-upstream-audit/prompt.md`
- Standing upstreams checked every run: `neovim/neovim`, `nix-community/nixvim`, `nvim-lua/kickstart.nvim`, `LazyVim/LazyVim`
- Rotating sample source: current `nix-community/nixvim` official user-config list; validate that entries still resolve and are active before counting them.
- Last audit: 2026-09-02 16:13 (Asia/Seoul), manual real test of the scheduled-task workflow.
- Last result: `refined`
- Current remote handoff candidate: `zaviro/nix-config#cloud/nixvim-workflow-upgrade@f0e90c6dddd98990d6b2e8cf888ec2089ca60317`
- Handoff base: `next@0794df868da3db02462f38de5e4bb8fa4c1fcc1c`

## Last run findings

- `ADD`: `splitkeep = "screen"`; native Neovim option with convergence across LazyVim and multiple active Nixvim configs.
- `ADD`: restore the last cursor location on ordinary file reopen; exclude `gitcommit` and `jjdescription` buffers.
- `KEEP`: native-first statusline, diagnostics, LSP, comment mappings, Treesitter, fzf-lua, Yazi, Flash, Conform, mini.ai/surround, guess-indent, checktime and Wayland clipboard support.
- `DEFER`: `jjsigns.nvim`; useful JJ semantics but currently immature enough that a mature config carries its own module and patch.
- `DEFER`: inlay-hint toggle; useful but still preference/noise-sensitive rather than a baseline requirement.
- `OMIT`: global `winborder = "rounded"`; primarily cosmetic.
- `OMIT`: project-local `exrc` as a default baseline; project/devenv configuration remains authoritative.
- No `flake.lock` update.
- Producer-side Nix/Neovim/atlas runtime validation was not available.

## Already audited rotating repos

### Initial audit — 2026-09-02

- `JMartJonesy/kickstart.nixvim`
- `GaetanLepage/nix-config`
- `wverac/nixvim`
- `XhuyZ/nixvim`
- `allen-liaoo/nvimx`
- `semi710/nvix`
- `Theaninova/TheaninovOS`
- `redyf/Neve`
- `spector700/Akari`
- `NikolayGalkin/gnvim`

### Scheduled-task real test — 2026-09-02

- `dc-tec/nixvim`
- `khaneliman/khanelivim`
- `MikaelFangel/nixvim-config`
- `rbpatt2019/minixvim`
- `Myxogastria0808/nix-flakes-nixvim`

## Known skipped official-list entries

- `ar-at-localhost/np` — 404 on 2026-09-02; not counted.
- `c4patino/nixvim` — 404 on 2026-09-02; not counted.
- `nicolas-goudry/nixvim-config` — repository exists but last meaningful push observed in 2024; not counted as an active rotating sample on 2026-09-02.

## Decision standard

Prefer native Neovim capabilities; accept changes for compatibility/breakage, native replacement of plugins, clear high-frequency workflow improvements, or strong cross-upstream convergence. Avoid single-source novelty, cosmetic-only additions, duplicated capabilities, unnecessary distribution-style complexity, and Git-centric behavior that conflicts with the JJ-first workflow. Look for removals/replacements as actively as additions.

## Next run

Read `prompt.md`, `status.md`, and `history.jsonl` first. Re-check standing upstream changes since this run, then choose 5–8 different active repositories from the current official Nixvim user-config list. Validate existence/activity before counting them, and avoid all repositories listed above unless a material change or specific capability comparison justifies revisiting one.
