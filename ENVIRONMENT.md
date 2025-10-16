# Local Environment Information

The following information is for AI Agents to learn specifics of the user and environment they are running in.

**Instructions**: Customize this file with your personal information, system configuration, and preferences. This helps AI agents provide more contextual and relevant assistance.

## User

- Name: [Your Name]
- Skills: [Your primary skills and expertise areas]
- Language: [Your preferred language and dialect, e.g., American English, British English]
- Location: [Your city, state/province, country]
- Company: [Your company name, if applicable]
- Document Style: [Your preferred documentation format, e.g., CommonMark, GitHub Flavored Markdown]

## Operating System

- OS: [Your OS and version, e.g., macOS Sequoia 15.0, Ubuntu 22.04 LTS, Windows 11]
- CPU: [Your CPU model and specs]
- Memory: [Your system memory]
- Shell: [Your shell and version, e.g., bash 5.2.15, zsh 5.9]
- Architecture: [Your system architecture, e.g., x86_64, arm64]
- Locale: [Your system locale, e.g., en_US.UTF-8, en_GB.UTF-8]

## Terminal

- Terminal Emulator: [Your terminal application and version, e.g., iTerm2 3.5.0, Alacritty 0.13.0, Windows Terminal 1.18]
- Terminal type: [Your TERM variable, e.g., `xterm-256color`, `alacritty`]
- Color support: [Your color capabilities, e.g., 256 colors, truecolor]
- Font: [Your preferred terminal font, e.g., JetBrains Mono, Fira Code, Cascadia Code]
- Additional features: [Any special features or configuration notes]

## Reference Documentation

- Commonly used documentation is cloned to the local system for easy reference
- Default Path: `~/reference` (customize to your preferred location)
- Index:
  - Main Index: `~/reference/INDEX.csv`
  - Child Index: Each documentation directory contains an INDEX.csv file

Querying indexes:

- Read CSV files directly using the Read tool (most token-efficient)
- Use Ripgrep for keyword searches: `rg -i "keyword" ~/reference/*/INDEX.csv`
- Use fd for document searches: `fd --type f "pattern" ~/reference`
- Example: `rg -i "yaml" ~/reference/*/INDEX.csv` to find YAML-related docs

## CLI Tools

Preferred CLI tools are available on the system. See `docs/tools.md` for a comprehensive list and customize it with your installed tools.

Key preferences (customize with your preferred tools):

- Use Ripgrep `rg` instead of grep (faster, better defaults)
- Use `fd` for finding files instead of find (faster, simpler syntax)
- Use `bat` for viewing files with syntax highlighting (optional)
- Use `lsd` or `exa` for enhanced directory listings (optional)

Directory tree examples:

- With lsd: `lsd --tree --depth <n> [dir]`
- With exa: `exa --tree --level <n> [dir]`
- Standard: `tree -L <n> [dir]`

## Custom Commands (Optional)

This section is for any custom commands or aliases you've created.

Examples:

- `my-search <terms>`: Custom search wrapper
- `my-fetch <url>`: Custom web page fetcher
- Add your own custom commands here

## Additional Reference Documentation

- **~/reference/docs/tools.md**: Comprehensive list of installed CLI tools (customize this file)
- **~/reference/docs/source.md**: External documentation sources and setup
