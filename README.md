# Dotfiles

Personal dotfiles for macOS development, optimized for PHP/Laravel development in 2026.

> Forked from [freekmurze/dotfiles](https://github.com/freekmurze/dotfiles) by [Freek Van der Heurck](https://freek.dev) (Spatie). Cleaned up and customized for personal use.

## Installation

```bash
git clone git@github.com:thecrazybob/dotfiles.git ~/.dotfiles
source ~/.zshrc
```

## Structure

```
~/.dotfiles/
├── shell/
│   ├── .aliases      # Command shortcuts
│   ├── .exports      # Environment variables
│   ├── .functions    # Shell functions
│   ├── .zshrc        # Zsh configuration
│   ├── .global-gitignore
│   └── z.sh          # Directory jumper
├── macos/
│   └── set-defaults.sh  # macOS preferences
├── claude/
│   ├── settings.json    # Claude Code preferences & plugins
│   ├── statusline.sh    # Custom status line script
│   └── commands/        # Custom slash commands
│       └── interview.md
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

### PHP Version Switching

| Alias | Description |
|-------|-------------|
| `switch-php83` | Switch to PHP 8.3 |
| `switch-php84` | Switch to PHP 8.4 |

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

### Claude

| Alias | Description |
|-------|-------------|
| `ccd` | Claude with `--dangerously-skip-permissions` |
| `claude-vacatia` | Claude with alternate config directory |
| `claude-usage` | Check Claude API usage |

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

```bash
cd ~/.dotfiles/macos
./set-defaults.sh
```

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
- PHP 8.4 (`/opt/homebrew/opt/php@8.4/bin`)
- MySQL from DBngin
- Bun (`~/.bun/bin`)

---

## Claude Code Setup

After cloning, symlink Claude configs to use dotfiles versions:

```bash
# Create ~/.claude if it doesn't exist
mkdir -p ~/.claude

# Backup existing configs (if any)
[ -f ~/.claude/settings.json ] && mv ~/.claude/settings.json ~/.claude/settings.json.bak
[ -f ~/.claude/statusline.sh ] && mv ~/.claude/statusline.sh ~/.claude/statusline.sh.bak
[ -d ~/.claude/commands ] && mv ~/.claude/commands ~/.claude/commands.bak

# Create symlinks
ln -sf ~/.dotfiles/claude/settings.json ~/.claude/settings.json
ln -sf ~/.dotfiles/claude/statusline.sh ~/.claude/statusline.sh
ln -sf ~/.dotfiles/claude/commands ~/.claude/commands
```

**What's tracked:**
- `settings.json` - Permissions, plugins, statusline config
- `statusline.sh` - Custom status bar (model, context usage, git info, cost)
- `commands/` - Custom slash commands like `/interview`

**What's NOT tracked (for security):**
- `history.jsonl` - Contains conversation history
- `projects/`, `todos/`, `shell-snapshots/` - Session data

---

## Customization

For machine-specific configs that shouldn't be committed, create files in `~/.dotfiles-custom/shell/`:

```bash
mkdir -p ~/.dotfiles-custom/shell
touch ~/.dotfiles-custom/shell/.aliases
touch ~/.dotfiles-custom/shell/.exports
```

These are automatically sourced by `.zshrc`.
