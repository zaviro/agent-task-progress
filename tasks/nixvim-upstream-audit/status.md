# Nixvim upstream audit

- Task ID: `nixvim-upstream-audit`
- Cadence: monthly
- Target config: `zaviro/nix-config`
- Standing upstreams checked every run: `neovim/neovim`, `nix-community/nixvim`, `nvim-lua/kickstart.nvim`, `LazyVim/LazyVim`
- Rotating sample source: current `nix-community/nixvim` official user-config list; prefer 5-8 active repos not used in the latest audits.
- Last audit date: 2026-09-02 (Asia/Seoul)
- Last result: audited baseline refined; current remote handoff candidate is `zaviro/nix-config#cloud/nixvim-workflow-upgrade@1d3020dae29837864b112e8e3c64838386f8dd84`.

## Already audited rotating repos

- `JMartJonesy/kickstart.nixvim` — 2026-09-02
- `GaetanLepage/nix-config` — 2026-09-02
- `wverac/nixvim` — 2026-09-02
- `XhuyZ/nixvim` — 2026-09-02
- `allen-liaoo/nvimx` — 2026-09-02
- `semi710/nvix` — 2026-09-02
- `Theaninova/TheaninovOS` — 2026-09-02
- `redyf/Neve` — 2026-09-02
- `spector700/Akari` — 2026-09-02
- `NikolayGalkin/gnvim` — 2026-09-02

## Decision standard

Prefer native Neovim capabilities; accept changes for compatibility/breakage, native replacement of plugins, clear high-frequency workflow improvements, or cross-upstream consensus. Avoid adding single-source novelty, cosmetic-only plugins, duplicated capabilities, or Git-centric behavior that conflicts with the JJ-first workflow. On each run, look for removals/replacements as well as additions.

## Next run

Read `history.jsonl` first, then choose different rotating repositories where practical. Re-check previously audited repos only when they have materially changed or when a capability under review requires comparison.
