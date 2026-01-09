---
name: chezmoi
description: Manage dotfiles with chezmoi. Use when working with dotfiles, chezmoi templates, machine-specific configuration, or when the user mentions chezmoi.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash(chezmoi:*)
---

# Chezmoi Dotfiles Management

## Commands

```bash
chezmoi add <file>           # Add file to chezmoi
chezmoi apply --refresh-externals --force  # Apply changes (always use these flags)
chezmoi diff                 # Preview what would change
chezmoi cat <file>           # Preview rendered template output
chezmoi data                 # Show available template variables
chezmoi edit <file>          # Edit source file
```

## File Naming

| Prefix/Suffix | Effect |
|---------------|--------|
| `dot_` | Installed as `.` (`dot_gitconfig` → `~/.gitconfig`) |
| `private_` | Restrictive permissions (600) |
| `executable_` | Executable permissions (755) |
| `.tmpl` | Processed as Go template |
| `symlink_` | Creates symlink |

## Machine-Specific Templates

Convert a static file to a template by renaming with `.tmpl` suffix, then use conditionals:

### By OS
```
{{- if eq .chezmoi.os "darwin" }}
# macOS config
{{- end }}

{{- if eq .chezmoi.os "linux" }}
# Linux config
{{- end }}
```

### By hostname
```
{{- if hasPrefix .chezmoi.hostname "work-" }}
# work machine config
{{- end }}
```

### By environment variable
```
{{- if env "WORK_ENV" }}
# when WORK_ENV is set
{{- end }}
```

### Combined conditions
```
{{- if or (eq .chezmoi.os "darwin") (env "WORK_ENV") }}
# macOS or when WORK_ENV is set
{{- end }}
```

## Escaping Nested Templates

When the target file uses `{{ }}` syntax (like mise, Jinja, Tera):

```
SOME_VAR = "{{ "{{" }}env.OTHER_VAR{{ "}}" }}"
```

This renders as `SOME_VAR = "{{env.OTHER_VAR}}"` in the output.

## External Dependencies

Manage external git repos in `.chezmoiexternal.toml`:

```toml
[".zsh/plugins/some-plugin"]
    type = "git-repo"
    url = "https://github.com/user/some-plugin.git"
    refreshPeriod = "168h"
```

## Gotchas

1. **No auto-delete**: Files removed from source need manual cleanup at destination
2. **Always preview**: Run `chezmoi cat <file>` before applying templates
3. **Always use flags**: Use `chezmoi apply --refresh-externals --force` to ensure externals refresh and no TTY prompts
4. **Template errors**: Use `chezmoi execute-template` to debug template syntax
