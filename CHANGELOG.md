# Changelog

All notable changes to **useful_tmux_commands** are documented here.

This project has no formal releases or semantic versioning. There are no tags or GitHub releases. Changes are tracked by commit date against the `main` branch.

Repository: <https://github.com/Dicklesworthstone/useful_tmux_commands>

---

## 2026-02-21 / 2026-02-22 -- License and Branding

### License Overhaul

Replaced the plain MIT license with MIT + OpenAI/Anthropic Rider, which restricts use by OpenAI, Anthropic, and their affiliates without express written permission from Jeffrey Emanuel. Updated the README badge and prose to reflect the new license terms.

- [`ba7290c`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/ba7290c641f1d977e4de44e5752f197d10503020) -- update LICENSE file to MIT with OpenAI/Anthropic Rider
- [`c1ca16a`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/c1ca16a4652e6bc174e2327390dc3b3515723469) -- update README license badge and references

### Social Preview Image

Added a 1280x640 Open Graph image (`gh_og_share_image.png`) for consistent social media link previews when sharing the repository URL.

- [`06f2ab4`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/06f2ab4da52d5cae86f185e83604cb9098a927fc)

---

## 2026-01-21 -- Initial License

Added the initial MIT License file to the repository.

- [`aa1bfe7`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/aa1bfe7d2f2f630adee189bbf1e5e2a8094aa7de)

---

## 2026-01-17 -- Documentation Corrections

Minor README fixes (4 lines changed) for documentation consistency. No functional changes.

- [`4597691`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/4597691a86c4444d336ab6b802fdd4a8aaf537a4)

---

## 2025-12-09 / 2025-12-10 -- Initial Build

The entire toolkit was created and refined in a single evening session spanning 12 commits across approximately four hours, from the initial 1,423-line script to a fully-featured command palette system with easy-mode installer.

### Core Session Management

The foundational `add_useful_tmux_commands_to_zshrc.sh` installer script, which appends all functions and aliases to `~/.zshrc` inside marker-delimited blocks (`NAMED-TMUX-COMMANDS-START` / `NAMED-TMUX-COMMANDS-END`).

- [`f9c39cf`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/f9c39cf0e2d2dfdf975cab3fe0bb9fae2a521311) -- initial 1,423-line script with full session management toolkit

**Session lifecycle:**

| Command | Alias | Purpose |
|---------|-------|---------|
| `create-named-tmux` | `cnt` | Create empty session with N panes |
| `spawn-agents-in-named-tmux` | `sat` | Create session and launch Claude, Codex, and Gemini agents |
| `quick-project-setup` | `qps` | Create project directory, git init, and spawn agents in one step |
| `add-agents-to-named-tmux` | `ant` | Add more agents to an existing session |
| `reconnect-to-named-tmux` | `rnt` | Reattach to session (offers to create if missing) |
| `list-named-tmux` | `lnt` | List all tmux sessions |
| `status-named-tmux` | `snt` | Show pane details and agent counts |
| `view-named-tmux-panes` | `vnt` | Unzoom, tile layout, and attach |
| `zoom-pane-in-named-tmux` | `znt` | Zoom to specific pane by index or agent type |
| `kill-named-tmux` | `knt` | Kill session with confirmation (`-f` to force) |

**Agent interaction:**

| Command | Alias | Purpose |
|---------|-------|---------|
| `broadcast-prompt` | `bp` | Send prompt to agents by type (`cc`, `cod`, `gmi`, `all`) with optional `--stagger=N` |
| `send-command-to-named-tmux` | `sct` | Send command to panes with filters (`--cc`, `--cod`, `--gmi`, `-s` skip first) |
| `interrupt-agents-in-named-tmux` | `int` | Send Ctrl+C to all agent panes |

**Output capture:**

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

**Infrastructure included in the initial commit:**

- `check-agent-deps` / `cad` -- verify Claude, Codex, and Gemini CLIs are installed
- `ntm` -- colorized help table with all commands and examples
- Pane naming convention: `<project>__<agent>_<number>` (e.g., `myproject__cc_1`)
- Auto-detection of project base directory: `~/Developer` (macOS) or `/data/projects` (Linux), overridable via `$PROJECTS_BASE`
- Idempotent installer with zshrc backup
- Oh My Zsh + Powerlevel10k installation offered for first-time zsh users
- Auto-install of tmux via system package manager when missing
- Session name validation (rejects `:` and `.` characters)
- Tab completion for session names via `compdef`

### Package Manager Detection

Simplified `apt-get`/`apt` detection logic by removing unnecessary variable assignments for a cleaner installation path.

- [`d4d0512`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/d4d05125e52bdd0579b2439842b57a05acdbbaf0)

### Log and Prompt Directory Defaults

Introduced XDG-compliant environment variables for organizing session data:

- `_NTM_LOG_DIR` -- defaults to `~/.local/share/ntm-logs`
- `_NTM_PROMPT_DIR` -- defaults to `~/.local/state/ntm-prompts`

Also added the initial `README.md` (comprehensive documentation) and `command_palette.md` (sample configuration with 32 entries).

- [`3aca1ec`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/3aca1ec7789b687774baf50f0b580bd6287f9dca)

### Command Palette System

Added a full fzf-powered command palette system (+848 lines) providing a fuzzy-searchable interface for pre-configured prompts, invocable with a single keystroke. The palette reads from a Markdown-based config file at `~/.config/ntm/command_palette.md`, supporting both a heading-based format and a legacy table format.

- [`d994d4f`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/d994d4f82d898e012d947c90c14c5d6e45b2b22e) -- core palette implementation

**New commands:**

| Command | Alias | Purpose |
|---------|-------|---------|
| `ntm-palette` | `ncp` | Open fzf palette for a session |
| `ntm-palette-interactive` | `ncpi` | Fully interactive palette (designed for tmux popup) |
| `ntm-palette-init` | `ncpinit` | Create sample `~/.config/ntm/command_palette.md` |
| `ntm-palette-bind` | `ncpbind` | Bind F6 key to open palette in tmux popup |
| `ntm-palette-quick` | `ncpq` | Simple numbered menu (no fzf dependency required) |

**Internal functions:** `_ntm_parse_palette_config`, `_ntm_parse_legacy_palette`, `_ntm_load_palette_commands`, `_ntm_check_fzf`, `_ntm_auto_install_fzf`, `_ntm_ensure_fzf`.

### Easy Mode Installer

Added `--easy` flag to the curl-pipe-bash installer for full one-command setup (+522 lines). Running `bash -s -- --easy` automatically:

- Installs tmux and fzf via the system package manager
- Applies recommended `tmux.conf` settings (mouse support, 256 colors, status bar)
- Sets up the F6 keybinding for the command palette
- Fetches the default `command_palette.md` from the repo

Also added visual infrastructure for the palette UI:

- `_ntm_has_nerd_fonts` -- detect Nerd Font availability for rich icon display
- `_ntm_init_icons` -- initialize icon set with Unicode fallbacks
- `_ntm_init_colors` -- Catppuccin color theme initialization
- `_ntm_show_target_menu` -- visual target selector with color-coded agent types
- `_ntm_show_pane_selector` -- interactive pane selection UI

Commit: [`7e3e47a`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/7e3e47ab44480d8b3e5dfd01f8852a670e7b9f87)

### Command Palette Refinements

Four rapid commits polishing the palette system, sample configuration, and config fetching infrastructure:

**Improved sample config and display** -- expanded the default `command_palette.md` from 32 to approximately 120 entries organized by category; added `_ntm_default_pane_index` helper to honor tmux `pane-base-index` setting; improved label truncation for long command names in the tmux interface.

- [`6d6fc38`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/6d6fc38aebfb570683c96f0db0705c25d7699eda)

**Enhanced config fetching** -- refactored palette initialization and config download logic with `curl`-first, `wget`-fallback strategy; restructured `command_palette.md` categories; added instructions for customizing defaults by forking the repo.

- [`b35f5b3`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/b35f5b334e9ff979269743214a8954660c3a3459)

**Pane output validation** -- added numeric validation for pane index arguments; refined download error handling; expanded palette entries.

- [`81630ee`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/81630eea1e9c471d322017853b1ad37386d58c15)

**Offline fallback** -- added embedded fallback palette that is written to disk when remote `command_palette.md` fetch fails, ensuring a functional setup without network access.

- [`fe76168`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/fe7616876b079e9521ba810e57b5fc378ad8bd95)

### Config Fetch and Write Functions

Introduced `fetch_default_palette()` and `write_sample_palette()` as top-level installer functions, cleanly separating the download logic (curl/wget with fallback) from the embedded sample writer. Both are invoked during easy-mode installation.

- [`eb013c3`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/eb013c3ae1308b6817f0d5a6ad7fb45c2f716364)

### Keybinding and Configuration Handling

Improved the F6 keybinding to use `zsh -ic` for proper interactive shell mode inside the tmux popup. Added a `backup_file()` utility for safe config file backups. Refined `.tmux.conf` detection and creation logic with better error handling and user feedback.

- [`216a86c`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/216a86c5befe17407125d30e75698db61617f639)

### Example Consistency

Replaced all `slidechase` references with `myproject` across command examples in the help text, aligning with README documentation.

- [`4f6f5a2`](https://github.com/Dicklesworthstone/useful_tmux_commands/commit/4f6f5a2c19a55a3c3f84cb7495900d0a10e9e7f1)

---

## File Inventory

| File | Purpose |
|------|---------|
| `add_useful_tmux_commands_to_zshrc.sh` | Installer script; appends all functions and aliases to `~/.zshrc` |
| `command_palette.md` | Default command palette configuration (fetched by installer) |
| `README.md` | Full documentation with command reference and architecture details |
| `LICENSE` | MIT License with OpenAI/Anthropic Rider |
| `gh_og_share_image.png` | GitHub social preview image (1280x640) |
