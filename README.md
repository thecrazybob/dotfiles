# Dotfiles

Personal dotfiles for macOS development environment.

## What's Included

### Shell Configuration (`shell/`)
- `.aliases` - Command shortcuts (git, php, npm, composer, claude, etc.)
- `.exports` - Environment variables and PATH configuration
- `.functions` - Helper shell functions
- `.zshrc` - Zsh configuration
- `.vimrc` - Vim configuration
- `.global-gitignore` - Global git ignore patterns
- `z.sh` - Directory jumping script

### macOS (`macos/`)
- `set-defaults.sh` - macOS system preferences
- `.mackup.cfg` - Mackup backup configuration

### Scripts
- `bootstrap` - Initial setup script
- `installscript` - Homebrew and tool installation

## Installation

```bash
git clone git@github.com:thecrazybob/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
./bootstrap
```

## Key Aliases

| Alias | Command |
|-------|---------|
| `a` | `php artisan` |
| `c` | `composer` |
| `ccd` | `claude --dangerously-skip-permissions` |
| `nah` | Reset git changes |
| `mfs` | `php artisan migrate:fresh --seed` |
| `pp` | `php artisan test --parallel` |

## Mackup

Settings are backed up to Google Drive via [Mackup](https://github.com/lra/mackup).
