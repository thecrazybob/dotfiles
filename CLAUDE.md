# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

Personal macOS dotfiles for a PHP/Laravel developer. There is no build, test, or lint pipeline — this is a configuration repo. Changes are applied to the live system via symlinks created during install (see `README.md` for the full link list). Editing a tracked file generally takes effect immediately in the next shell/Claude/Ghostty session.

## Layout and what each area drives

- `shell/` — Sourced by `~/.zshrc` (which is itself a symlink to `shell/.zshrc`). `.zshrc` sources `.exports`, `.aliases`, `.functions` in that order, then sources the same files from `~/.dotfiles-custom/shell/` for machine-local overrides that are intentionally not tracked. `z.sh` is the directory jumper.
- `claude/` — Symlinked into `~/.claude/`. `settings.json` is the user-level Claude Code config (env vars, permissions allow-list, enabled plugins, marketplaces, statusline). `commands/`, `agents/`, `skills/` are user-level slash commands, subagents, and skills. Many entries under `claude/skills/` are symlinks into `~/.agents/skills/` (the impeccable plugin's shared store) — treat those as read-only from this repo's perspective.
- `opencode/` — Symlinked into `~/.config/opencode/`. `package.json` + `bun.lock` are installed with `bun install` after symlinking.
- `ghostty/config` — Symlinked into `~/Library/Application Support/com.mitchellh.ghostty/config`.
- `karabiner/` — Karabiner-Elements config.
- `macos/set-defaults.sh` — One-shot script that writes a large set of `defaults` keys (Finder, Dock, Safari, input, etc.) and uses `sudo nvram StartupMute=%01` for the boot sound. Re-run after editing.
- `Brewfile` — Source of truth for Homebrew packages, casks, and taps. Apply with `brew bundle --file=~/.dotfiles/Brewfile`. A few apps are deliberately *not* in the Brewfile (Bear, Things 3, Xcode, Beeper) — see the comment block at the bottom of the file.

## Things that are easy to get wrong

- **`xdebug()` in `.functions` targets `${conf.d}/ext-xdebug.ini`**, located via `php --ini`. It assumes xdebug was installed via `pecl install xdebug` (which writes that file). If a user installs xdebug a different way or wants to toggle the line in the main `php.ini` instead, the function will report "not found" even though xdebug is loaded. Don't "helpfully" make it grep `php.ini` as a fallback — that's the bug we just removed.
- **`server()` in `.functions` requires Python 3** (`python3` on PATH, which Homebrew or Xcode CLT provides). The heredoc subclasses `http.server.SimpleHTTPRequestHandler` — if you edit it, preserve the heredoc form (`python3 - "$port" <<'PYEOF'`) to avoid quoting hell with `$` and backslashes.
- **PATH ordering in `.zshrc` matters.** `~/.local/bin` is appended *after* nvm so the native Claude Code binary takes priority over any npm-installed `claude`. Don't reorder these blocks casually.
- **Custom overrides live in `~/.dotfiles-custom/shell/`**, not in this repo. If a user reports an alias/function behaving differently than what's tracked here, check there first.
- **Global gitignore** is `shell/.global-gitignore` (symlinked to `~/.global-gitignore`). Adding patterns here affects every repo on the machine.
- **macOS `sed -i` requires the empty-string argument**: `sed -i '' 's/.../.../g' file`. Writing `sed -i -e '...'` (the GNU/BSD-portable form some people reach for) creates a stray backup file named `-e` on macOS. The repo has been bitten by this once — keep using `sed -i ''`.

## Conventions

- The `commit()` function in `shell/.functions` does `git add .` and, if no message is passed, pipes the staged diff to `claude -p` to generate a conventional-commit message. Existing repo commits follow that `type: description` format (`chore:`, `fix:`, `feat:`, …) — match it when committing here.
- Aliases live in `.aliases`, multi-line shell logic lives in `.functions`. Don't put functions in `.aliases`.
- The Claude `settings.json` `permissions.allow` list is curated — only Bash patterns and MCP tools the user has explicitly approved live there. Don't add to it speculatively.
- `enabledPlugins` in `settings.json` is the source of truth for which plugins are active; the matching `extraKnownMarketplaces` block is what makes them installable. Adding a plugin requires both.

## Keep documentation in sync

Whenever you change a tracked file in this repo, update the relevant documentation in the **same** change — never leave it for later:

- **`README.md`** is user-facing. If you add/remove/rename an alias, function, env var, PATH entry, symlink in the install steps, or anything in the `Structure` tree, update the matching table or section. The alias/function tables in `README.md` are the public reference — they must match `shell/.aliases` and `shell/.functions` exactly.
- **`CLAUDE.md`** (this file) is the agent's map. If you change *how* something works in a way that affects the "Things that are easy to get wrong", "Conventions", or "Layout" sections — fix the relevant bullet. If you fix one of the documented footguns (the dead `misc/oh-my-zsh-custom` ref, the hardcoded PHP 7.4 path in `xdebug()`, the Python 2 `SimpleHTTPServer` in `server()`), remove its bullet from the footgun list.
- **`Brewfile`** comments at the bottom list manual installs — keep them accurate if you add/remove anything from those categories.
- **`settings.json` `enabledPlugins` / `extraKnownMarketplaces`** — when toggling plugins, both blocks need to stay consistent.

If a change touches behavior that isn't documented anywhere yet but *should* be (a new footgun, a new convention, a non-obvious ordering requirement), add it to `CLAUDE.md` in the same change. Don't ship undocumented surprises.

## Applying changes

- Shell edits: `source ~/.zshrc` (or open a new shell).
- Claude config edits: restart Claude Code (the file is read at startup).
- macOS defaults: re-run `cd ~/.dotfiles/macos && ./set-defaults.sh`. Some keys require logout/restart of the affected app (Finder, Dock) to take effect; the script does some `killall` calls but not all.
- Brewfile edits: `brew bundle --file=~/.dotfiles/Brewfile` (additive — won't uninstall removed entries unless run with `--cleanup`).
