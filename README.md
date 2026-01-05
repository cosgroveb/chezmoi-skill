# chezmoi-skill

A Claude Code skill that teaches Claude how to manage dotfiles with [chezmoi](https://www.chezmoi.io/), including machine-specific configuration.

## Installation

### Manual

```bash
git clone https://github.com/cosgroveb/chezmoi-skill.git ~/.claude/skills/chezmoi
```

### Via chezmoi

Add to your `.chezmoiexternal.toml`:

```toml
[".claude/skills/chezmoi"]
    type = "git-repo"
    url = "https://github.com/cosgroveb/chezmoi-skill.git"
    refreshPeriod = "168h"
```

Then run `chezmoi apply`.

## What It Does

This skill activates when you mention "dotfiles" or "chezmoi" and helps Claude:

- Add and manage files with chezmoi
- Convert static configs to machine-specific templates
- Use conditional blocks for OS, hostname, or environment variables
- Handle nested template syntax (mise, Jinja, etc.)
- Preview and apply changes safely

## Example Usage

```
"Add my gitconfig to chezmoi"
"Make this config only apply on macOS"
"Convert this to a chezmoi template with work/personal conditions"
"Why isn't my config applying?"
```

## License

MIT
