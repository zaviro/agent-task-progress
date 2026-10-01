# Nixvim upstream audit

- Task ID: `nixvim-upstream-audit`
- Cadence: monthly
- Target config: `zaviro/nix-config`
- Canonical task specification: `tasks/nixvim-upstream-audit/prompt.md`
- Standing upstreams checked every run: `neovim/neovim`, `nix-community/nixvim`, `nvim-lua/kickstart.nvim`, `LazyVim/LazyVim`
- Rotating sample source: current `nix-community/nixvim` official user-config list; validate that entries still resolve and are active before counting them.
- Last audit: 2026-10-02 07:11 (Asia/Shanghai)
- Last result: `no-change`
- Current authoritative config ref: `zaviro/nix-config#main`
- Previous handoff `cloud/nixvim-workflow-upgrade@f0e90c6dddd98990d6b2e8cf888ec2089ca60317` is no longer a live branch; the current `main` already contains the audited `splitkeep` and last-location changes.

## Current run

Standing upstream heads observed:
- `neovim/neovim@d0596fa4429c0a5e2bd83057cd9e713b5b4587de`
- `nix-community/nixvim@5980a626794486abad69fca7667f9c11dfbc3bd7`
- `nvim-lua/kickstart.nvim@80743df53d8f7058fc5b60e41f1081d11df9c880`
- `LazyVim/LazyVim@999700997f72227187d49d8b92667183dc7fc809`

Rotating repositories audited:
- `Ahwxorg/nixvim-config` — active; last push 2026-08-14
- `alisonjenkins/neovim-nix-flake` — active; last push 2026-10-01
- `carl0xs/nixcfg` — active; last push 2026-09-16
- `literally-sai/vermvim` — active; last push 2026-09-02
- `mathjiajia/nix-darwin` — active; last push 2026-09-28
- `pete3n/nixvim-flake` — active; last push 2026-06-06
- `siph/nixvim-flake` — active; last push 2026-09-01
- `traxys/Nixfiles` — active; last push 2026-09-27
- `ZainKergaye/nixosdotfiles` — active; last push 2026-09-29

## Findings

- `KEEP`: current native-first baseline remains appropriate.
- `KEEP`: `splitkeep = "screen"` and last-location restore are already integrated on `main`.
- `DEFER`: native multicursor deserves future UX review because Neovim now owns it, but the user's `Ctrl-h/j/k/l` window-navigation scheme conflicts with Neovim's `Ctrl-l` multicursor-clear mapping; current mature Nixvim samples also retain `Ctrl-l` for right-window navigation. No change this run.
- `DEFER`: Neovim's improved external-file watcher/autoread work is on the 0.13 roadmap, but the Nixvim pinned nixpkgs currently resolves Neovim 0.12.5, so the existing `checktime` autocmd remains justified for the current baseline.
- `DEFER`: Nixvim added native LSP feature toggles and a `plugins.hover` module upstream; neither creates a concrete gap in the current workflow.
- `DEFER`: LazyVim has 0.13-specific `vim.hl.hl_op` compatibility work, but current Nixvim nixpkgs is 0.12.5; revisit when the pinned runtime moves.
- No accepted ADD/REMOVE/REPLACE change.
- No `/rh` handoff created.
- No `flake.lock` update.
- No atlas/Nix/Neovim runtime validation claimed.

## Previously audited rotating repos

### 2026-09-02 initial audit
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

### 2026-09-02 scheduled-task real test
- `dc-tec/nixvim`
- `khaneliman/khanelivim`
- `MikaelFangel/nixvim-config`
- `rbpatt2019/minixvim`
- `Myxogastria0808/nix-flakes-nixvim`

### 2026-10-02 scheduled audit
- `Ahwxorg/nixvim-config`
- `alisonjenkins/neovim-nix-flake`
- `carl0xs/nixcfg`
- `literally-sai/vermvim`
- `mathjiajia/nix-darwin`
- `pete3n/nixvim-flake`
- `siph/nixvim-flake`
- `traxys/Nixfiles`
- `ZainKergaye/nixosdotfiles`

## Known skipped official-list entries

- `elythh/nixvim` — archived; not counted.
- `r17x/development-universe` — current repository lookup did not resolve; not counted.
- `bkp5190/Home-Manager-Configs`, `gwg313/nvim-nix`, `hbjydev/hvim`, `Tanish2002/neovim-config`, `Yohh/nix-confix` — resolved but last meaningful activity was outside the roughly 12-month active window; not counted.

## Next run

Read `prompt.md`, `status.md`, and `history.jsonl` first. Re-check standing upstream changes since this run, then choose 5–8 different active repositories from the current official Nixvim user-config list. Validate existence/activity before counting them, and avoid all repositories listed above unless a material change or specific capability comparison justifies revisiting one.
