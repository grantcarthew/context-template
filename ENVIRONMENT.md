# Local Environment Information

## User

- Name: [Your Name]
- Skills: [Your primary skills and expertise areas]
- Language: [Your preferred language and dialect, e.g., American English, British English]
- Location: [Your city, state/province, country, (timezone)]
- Company: [Your company name, if applicable]
- Document Style: [Your preferred documentation format, e.g., CommonMark, GitHub Flavored Markdown]

## Desktop

- OS: [Your OS and version, e.g., EndeavourOS (Arch Linux) x86_64, macOS Tahoe 26.0 arm64, Ubuntu 22.04 LTS]
- Shell: [Your shell (don't include a version), e.g., Bash , Zsh]
- Package manager: [The package managers you are using, e.g., pacman/yay, apt, uv, brew/mise]

## Reference Repository

A curated collection of documentation and source code for AI agent context.

**Structure:**

- Global: ~/reference (system-wide references)
- Local: ./reference (project-specific references)
- Index: INDEX.csv in each directory (metadata about contents)

**Finding information:**

```bash
# Quick overview:
lsd --tree --depth 1 ~/reference

# Search by keyword:
rg -i "keyword" ~/reference/*/INDEX.csv

# Find files:
fd --type f --hidden --no-ignore 'filename'
```

**When to use:**

- Before using APIs or external services
- When you need project-specific examples
- When standard knowledge seems insufficient

For more information read ~/reference/AGENTS.md

## Preferred CLI Tools

- `rg` (ripgrep) instead of grep
- `lsd --tree --depth <n>` for directory trees
- `fd` for finding files

## Fetch Internet Content

- `kagi <search-terms>`: Search the internet returning clean search results
- `snag <url>`: Fetch web page content in Markdown via a browser
- `curl https://raw.githubusercontent.com/{username}/{repository}/{branch}/{path_to_file}`: GitHub file content
