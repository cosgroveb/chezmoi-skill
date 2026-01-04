# chezmoi-skill

A Claude Code plugin that teaches Claude how to manage dotfiles with [chezmoi](https://www.chezmoi.io/), including machine-specific configuration.

## Installation

```bash
# Add the marketplace
/plugin marketplace add cosgroveb/chezmoi-skill

# Install the skill
/plugin install chezmoi@chezmoi-skill
```

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
