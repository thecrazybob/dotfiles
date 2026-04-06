# Dotfiles

Personal dotfiles for macOS development, optimized for PHP/Laravel development in 2026.

> Forked from [freekmurze/dotfiles](https://github.com/freekmurze/dotfiles) by [Freek Van der Heurck](https://freek.dev) (Spatie). Cleaned up and customized for personal use.

## Installation

```bash
# 1. Clone
git clone git@github.com:thecrazybob/dotfiles.git ~/.dotfiles

# 2. Install Homebrew + packages
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew bundle --file=~/.dotfiles/Brewfile

# 3. Oh-My-Zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# 4. Symlink shell configs
ln -sf ~/.dotfiles/shell/.zshrc ~/.zshrc
ln -sf ~/.dotfiles/shell/.gitconfig ~/.gitconfig
ln -sf ~/.dotfiles/shell/.global-gitignore ~/.global-gitignore
mkdir -p ~/.ssh
ln -sf ~/.dotfiles/shell/.ssh-config ~/.ssh/config

# 5. Symlink Claude Code configs
mkdir -p ~/.claude
ln -sf ~/.dotfiles/claude/settings.json ~/.claude/settings.json
ln -sf ~/.dotfiles/claude/statusline.sh ~/.claude/statusline.sh
ln -sf ~/.dotfiles/claude/commands ~/.claude/commands
ln -sf ~/.dotfiles/claude/agents ~/.claude/agents
ln -sf ~/.dotfiles/claude/skills ~/.claude/skills

# 6. Symlink Ghostty config
mkdir -p ~/Library/Application\ Support/com.mitchellh.ghostty
ln -sf ~/.dotfiles/ghostty/config ~/Library/Application\ Support/com.mitchellh.ghostty/config

# 7. Symlink OpenCode config
mkdir -p ~/.config/opencode
ln -sf ~/.dotfiles/opencode/commands ~/.config/opencode/commands
ln -sf ~/.dotfiles/opencode/package.json ~/.config/opencode/package.json
ln -sf ~/.dotfiles/opencode/bun.lock ~/.config/opencode/bun.lock
cd ~/.config/opencode && bun install

# 8. macOS defaults
cd ~/.dotfiles/macos && ./set-defaults.sh

# 9. Load shell
source ~/.zshrc
```

## Structure

```
~/.dotfiles/
├── Brewfile              # Homebrew packages, casks & apps
├── shell/
│   ├── .aliases          # Command shortcuts
│   ├── .exports          # Environment variables
│   ├── .functions        # Shell functions
│   ├── .gitconfig        # Global git configuration
│   ├── .ssh-config       # SSH host configuration
│   ├── .zshrc            # Zsh configuration
│   ├── .global-gitignore
│   └── z.sh              # Directory jumper
├── macos/
│   └── set-defaults.sh   # macOS preferences
├── claude/
│   ├── settings.json     # Claude Code preferences & plugins
│   ├── statusline.sh     # Custom status line script
│   ├── commands/         # Custom slash commands
│   ├── agents/           # Custom subagent definitions
│   └── skills/           # Custom skill definitions
├── opencode/
│   ├── package.json      # OpenCode plugin dependencies
│   ├── bun.lock          # Bun lockfile
│   └── commands/         # Global slash commands
├── ghostty/
│   └── config            # Ghostty terminal configuration
└── README.md
```

---

## Aliases

### PHP/Laravel

| Alias | Command | Description |
|-------|---------|-------------|
| `a` | `php artisan` | Run artisan commands |
| `tinker` | `php artisan tinker` | Laravel REPL |
| `mfs` | `php artisan migrate:fresh --seed` | Reset database |
| `pp` | `php artisan test --parallel` | Run tests in parallel |
| `phpunit` | `vendor/bin/phpunit` | Run PHPUnit |
| `pint` | `vendor/bin/pint --dirty --parallel` | Format changed files |
| `stan` | `vendor/bin/phpstan analyse` | Static analysis |
| `sail` | `./vendor/bin/sail` | Laravel Sail |
| `aoc` | `php artisan optimize:clear` | Clear all caches |
| `livewire` | `php artisan livewire` | Livewire commands |

### Composer

| Alias | Command | Description |
|-------|---------|-------------|
| `c` | `composer` | Run composer |
| `cu` | `composer update` | Update packages |
| `cr` | `composer require` | Add package |
| `ci` | `composer install` | Install from lock |
| `cda` | `composer dump-autoload -o` | Regenerate autoloader |

### JavaScript

| Alias | Command |
|-------|---------|
| `ni` | `npm install` |
| `nrd` | `npm run dev` |
| `nrp` | `npm run prod` |
| `nrw` | `npm run watch` |
| `jest` | `./node_modules/.bin/jest` |

### Git

| Alias | Command | Description |
|-------|---------|-------------|
| `gc` | `git checkout` | Switch branches |
| `gpo` | `git push origin` | Push to origin |
| `gm` | `git merge` | Merge branches |
| `glog` | Pretty log | Graph with colors |
| `uncommit` | `git reset --soft HEAD~1` | Undo last commit, keep changes |
| `nah` | `git reset --hard; git clean -df` | Discard ALL changes |

### System

| Alias | Description |
|-------|-------------|
| `l` | Detailed file listing (`ls -laF`) |
| `o` | Open current folder in Finder |
| `show` / `hide` | Toggle hidden files in Finder |
| `ip` | Show public IP address |
| `localip` | Show local network IPs |
| `flushdns` | Clear DNS cache |
| `afk` | Lock screen |
| `emptytrash` | Empty trash + clear system logs |

### Dev Tools

| Alias | Description |
|-------|-------------|
| `phpstorm` | Open PhpStorm in current directory |
| `hostfile` | Edit `/etc/hosts` with nano |
| `sshconfig` | Edit SSH config with nano |
| `copykey` | Copy SSH public key to clipboard |
| `flush-redis` | Clear all Redis data |
| `php-log` | Open Valet PHP log |
| `nginx-log` | Open Valet nginx log |

### Forge

| Alias | Description |
|-------|-------------|
| `forge` | Laravel Forge CLI (suppresses PHP deprecation warnings) |

### Claude & AI

| Alias | Description |
|-------|-------------|
| `ccd` | Claude with `--dangerously-skip-permissions` |
| `claude-vacatia` | Claude with alternate config directory |
| `claude-usage` | Check Claude API usage |
| `codex-yolo` | Codex with `--dangerously-bypass-approvals-and-sandbox` |

### Worktree + AI Agents

| Alias | Description |
|-------|-------------|
| `wsc` | Create worktree and launch Claude Code |
| `wscv` | Create worktree and launch Claude (vacatia config) |
| `wscodex` | Create worktree and launch Codex |

---

## Functions

### Testing

```bash
p              # Run Pest (or PHPUnit fallback)
p --filter=foo # Run specific tests
pf foo         # Shorthand for --filter
```

### Database

```bash
db list              # List all databases
db create mydb       # Create database
db drop mydb         # Drop database
db refresh mydb      # Drop and recreate

opendb               # Parse .env and open DB in GUI client
```

### Git

```bash
commit "message"     # Add all + commit (uses aicommits if no message)
setg                 # Push with --set-upstream for current branch
git-prune-local      # Delete local branches not on remote (interactive)
```

### Laravel

```bash
tinker               # Open tinker REPL
tinker '$user'       # Execute and dd() result
scheduler            # Run scheduler in loop (local dev)
browse               # Open current project's .test URL
```

### Utilities

```bash
mkd dirname          # Create directory and cd into it
weather              # Weather forecast (default: Antwerp)
weather Dubai        # Weather for specific city
archive folder       # Create zip of folder
removehost hostname  # Remove SSH known host
server 8080          # Start Python HTTP server
phpserver 4000       # Start PHP built-in server
digga domain.com     # DNS lookup with all records
xdebug               # Toggle XDebug on/off
silent command       # Run command with suppressed output
```

---

## Directory Jumper (z)

`z` learns your most-used directories and lets you jump to them:

```bash
z sites              # Jump to most frecent match for "sites"
z scout              # Jump to directory matching "scout"
z foo bar            # Match both "foo" AND "bar"
z -l sites           # List all matches
z -r sites           # Jump to highest-ranked match
z -t sites           # Jump to most recent match
```

The more you visit a directory, the higher it ranks.

---

## macOS Defaults

Run `macos/set-defaults.sh` to configure macOS preferences:

- **Finder**: Show extensions, list view, POSIX path in title
- **Dock**: 72px icons, no bouncing, no indicator lights
- **System**: Disable autocorrect, smart quotes (better for coding)
- **Safari**: Enable developer tools
- **Timezone**: Europe/Istanbul

---

## Global Gitignore

Patterns in `shell/.global-gitignore` are ignored across all repos:

- macOS: `.DS_Store`, `.Spotlight-V100`, `.Trashes`
- IDEs: `.idea`, `.vscode`, `.sublime-project`
- Node: `node_modules`, `npm-debug.log`
- PHP: `.phpunit.result.cache`, `.phpunit-watcher-cache.php`
- Claude: `.claude`

---

## Environment

Key exports in `shell/.exports`:

| Variable | Value |
|----------|-------|
| `EDITOR` | `nano` |
| `HISTSIZE` | 32768 |
| `HOMEBREW_NO_AUTO_UPDATE` | 1 |

PATH includes:
- Homebrew (`/opt/homebrew/bin`)
- Composer (`~/.composer/vendor/bin`)
- Bun (`~/.bun/bin`)
- pnpm (`~/Library/pnpm`)
- NVM-managed Node
- Claude Code (`~/.local/bin`)

---

## What's NOT tracked (for security)

- `~/.npmrc` — contains npm auth token
- `~/.composer/auth.json` — OAuth tokens
- `~/.ssh/*` (private keys) — only the config is tracked
- `~/.claude/history.jsonl` — conversation history
- `~/.claude/projects/`, `todos/`, `shell-snapshots/` — session data

---

## Customization

For machine-specific configs that shouldn't be committed, create files in `~/.dotfiles-custom/shell/`:

```bash
mkdir -p ~/.dotfiles-custom/shell
touch ~/.dotfiles-custom/shell/.aliases
touch ~/.dotfiles-custom/shell/.exports
```

These are automatically sourced by `.zshrc`.

---

## Manual Installs

Apps not available via Homebrew:

- **Bear** — Mac App Store
- **Things 3** — Mac App Store
- **Xcode** — Mac App Store (`xcode-select --install` for CLI tools)
- **Beeper Desktop** — [beeper.com](https://beeper.com)

PHP versions and extensions are managed via **PHP Monitor** (installed via Brewfile).
