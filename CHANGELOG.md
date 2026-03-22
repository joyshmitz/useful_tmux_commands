# Changelog

All notable changes to **useful_tmux_commands** are documented here.

This project has no formal releases or semver tags. Changes are tracked by commit date.
Repository: <https://github.com/Dicklesworthstone/useful_tmux_commands>

---

## 2026-02-22 — License and Branding Update

### License

- Updated license from plain MIT to MIT with OpenAI/Anthropic Rider, restricting use by OpenAI, Anthropic, and affiliates without express written permission from Jeffrey Emanuel.
  [`ba7290c`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/ba7290c641f1d977e4de44e5752f197d10503020)
- Updated README license badge and references to reflect MIT + OpenAI/Anthropic Rider.
  [`c1ca16a`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/c1ca16a4652e6bc174e2327390dc3b3515723469)

### Branding

- Added GitHub social preview / Open Graph image (1280x640, `gh_og_share_image.png`).
  [`06f2ab4`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/06f2ab4da52d5cae86f185e83604cb9098a927fc)

---

## 2026-01-21 — MIT License Added

- Added initial MIT License file to the repository.
  [`aa1bfe7`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/aa1bfe7d2f2f630adee189bbf1e5e2a8094aa7de)

---

## 2026-01-17 — Documentation Cleanup

- Minor README corrections (4 lines changed, documentation consistency fixes).
  [`4597691`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/4597691a86c4444d336ab6b802fdd4a8aaf537a4)

---

## 2025-12-09 / 2025-12-10 — Initial Release

The entire toolkit was built and refined in a single evening (12 commits across ~4 hours).

### Core Session Management

Created the foundational `add_useful_tmux_commands_to_zshrc.sh` installer script (1,423 lines) providing a full tmux multi-agent orchestration toolkit appended to `~/.zshrc`.
[`f9c39cf`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/f9c39cf0e2d2dfdf975cab3fe0bb9fae2a521311)

**Session lifecycle commands:**

| Command | Alias | Purpose |
|---------|-------|---------|
| `create-named-tmux` | `cnt` | Create empty session with N panes |
| `spawn-agents-in-named-tmux` | `sat` | Create session and launch Claude/Codex/Gemini agents |
| `quick-project-setup` | `qps` | Create project dir, git init, spawn agents in one step |
| `add-agents-to-named-tmux` | `ant` | Add more agents to an existing session |
| `reconnect-to-named-tmux` | `rnt` | Reattach to session (offers to create if missing) |
| `list-named-tmux` | `lnt` | List all tmux sessions |
| `status-named-tmux` | `snt` | Show pane details and agent counts |
| `view-named-tmux-panes` | `vnt` | Unzoom, tile layout, and attach |
| `zoom-pane-in-named-tmux` | `znt` | Zoom to specific pane by index or agent type |
| `kill-named-tmux` | `knt` | Kill session (with confirmation; `-f` to force) |

**Agent interaction commands:**

| Command | Alias | Purpose |
|---------|-------|---------|
| `broadcast-prompt` | `bp` | Send prompt to agents by type (`cc`, `cod`, `gmi`, `all`); supports `--stagger=N` |
| `send-command-to-named-tmux` | `sct` | Send command to panes with filters (`--cc`, `--cod`, `--gmi`, `-s` skip first) |
| `interrupt-agents-in-named-tmux` | `int` | Send Ctrl+C to all agent panes |

**Output commands:**

| Command | Alias | Purpose |
|---------|-------|---------|
| `copy-pane-output` | `cpo` | Copy pane output to clipboard |
| `save-session-outputs` | `sso` | Save all pane outputs to timestamped log files |

**Agent CLI aliases:**

| Alias | Expands to |
|-------|------------|
| `cc` | `claude --dangerously-skip-permissions` (with 32GB Node heap) |
| `cod` | `codex --dangerously-bypass-approvals-and-sandbox -m gpt-5.1-codex-max` |
| `gmi` | `gemini --yolo` |

**Utilities:**

- `check-agent-deps` / `cad` — verify Claude, Codex, Gemini CLIs are installed.
- `ntm` — colorized help table with all commands and examples.
- Pane naming convention: `<project>__<agent>_<number>` (e.g., `myproject__cc_1`).
- Auto-detection of project base directory: `~/Developer` (macOS) or `/data/projects` (Linux), overridable via `$PROJECTS_BASE`.
- Idempotent installer with zshrc backup and marker-delimited block (`NAMED-TMUX-COMMANDS-START`/`END`).
- Oh My Zsh + Powerlevel10k installation offered for first-time zsh users.
- Auto-install of tmux via system package manager if missing.
- Session name validation (rejects `:` and `.` characters).
- Tab completion for session names via `compdef`.

### Package Manager Detection Fix

Simplified `apt-get`/`apt` detection logic (removed unnecessary variable assignments).
[`d4d0512`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/d4d05125e52bdd0579b2439842b57a05acdbbaf0)

### Log and Prompt Directory Defaults

Added XDG-compliant default paths for logs and stored prompts:
- `_NTM_LOG_DIR` defaults to `$XDG_DATA_HOME/ntm-logs` (`~/.local/share/ntm-logs`).
- `_NTM_PROMPT_DIR` defaults to `$XDG_STATE_HOME/ntm-prompts` (`~/.local/state/ntm-prompts`).

Also added the initial README.md and `command_palette.md` sample configuration.
[`3aca1ec`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/3aca1ec7789b687774baf50f0b580bd6287f9dca)

### Command Palette (fzf-powered)

Added a full command palette system (+848 lines) with five new commands:
[`d994d4f`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/d994d4f82d898e012d947c90c14c5d6e45b2b22e)

| Command | Alias | Purpose |
|---------|-------|---------|
| `ntm-palette` | `ncp` | Open fzf palette for a session |
| `ntm-palette-interactive` | `ncpi` | Fully interactive palette (for tmux popup use) |
| `ntm-palette-init` | `ncpinit` | Create sample `~/.config/ntm/command_palette.md` |
| `ntm-palette-bind` | `ncpbind` | Bind F6 key to open palette in tmux popup |
| `ntm-palette-quick` | `ncpq` | Simple numbered menu (no fzf dependency) |

Internal palette infrastructure: `_ntm_parse_palette_config`, `_ntm_parse_legacy_palette`, `_ntm_load_palette_commands`, `_ntm_check_fzf`, `_ntm_auto_install_fzf`, `_ntm_ensure_fzf`.

Config file format: Markdown-based at `~/.config/ntm/command_palette.md`, supporting both heading-based and legacy table formats.

### Easy Mode Installer

Added `--easy` flag to the installer for one-command setup (+522 lines):
[`7e3e47a`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/7e3e47ab44480d8b3e5dfd01f8852a670e7b9f87)

- Auto-installs tmux and fzf via system package manager.
- Applies recommended `tmux.conf` settings (mouse support, 256 colors, status bar).
- Sets up F6 keybinding for command palette.
- Fetches default `command_palette.md` from the repo.
- Nerd Font detection (`_ntm_has_nerd_fonts`) for rich icon display.
- Catppuccin color theme initialization (`_ntm_init_colors`).
- Visual target selector with color-coded agent types (`_ntm_show_target_menu`, `_ntm_show_pane_selector`).

### Palette Refinements (4 rapid commits)

**Improved sample config and display** — expanded default `command_palette.md` from 32 to ~120 entries organized by category; added `_ntm_default_pane_index` helper for honoring `pane-base-index`.
[`6d6fc38`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/6d6fc38aebfb570683c96f0db0705c25d7699eda)

**Enhanced config fetching** — refactored palette initialization and config download logic; restructured `command_palette.md` categories.
[`b35f5b3`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/b35f5b334e9ff979269743214a8954660c3a3459)

**Pane output validation** — improved command fetching logic with better error handling; added more palette entries.
[`81630ee`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/81630eea1e9c471d322017853b1ad37386d58c15)

**Offline fallback** — added offline/embedded fallback when remote `command_palette.md` fetch fails; refactored fetch flow.
[`fe76168`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/fe7616876b079e9521ba810e57b5fc378ad8bd95)

### Config Fetch and Write Functions

Added `fetch_default_palette()` and `write_sample_palette()` top-level functions to handle downloading and writing the default palette configuration, with proper error handling.
[`eb013c3`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/eb013c3ae1308b6817f0d5a6ad7fb45c2f716364)

### Keybinding and zshrc Handling Improvements

- F6 keybinding now uses `zsh -ic` for proper interactive shell mode in tmux popup.
- Added `backup_file()` utility for config file backups.
- Refined `.tmux.conf` detection and creation logic with better error handling.
[`216a86c`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/216a86c5befe17407125d30e75698db61617f639)

### Example Consistency

Replaced `slidechase` with `myproject` across all command examples in the help text for consistency with README documentation.
[`4f6f5a2`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/4f6f5a2c19a55a3c3f84cb7495900d0a10e9e7f1)

---

## File Inventory

| File | Purpose |
|------|---------|
| `add_useful_tmux_commands_to_zshrc.sh` | Installer script; appends all functions/aliases to `~/.zshrc` |
| `command_palette.md` | Default command palette configuration (fetched by installer) |
| `README.md` | Full documentation with command reference |
| `LICENSE` | MIT License with OpenAI/Anthropic Rider |
| `gh_og_share_image.png` | GitHub social preview image |
