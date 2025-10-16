# CLI Tools Reference

Instructions: This is a template file listing commonly useful CLI tools. Customize this file to reflect the tools installed on your system. This serves as a reference for AI agents to understand what tools are available.

## How to Use This Template

1. Review the tools listed below
2. Remove tools you don't have installed
3. Add tools specific to your workflow
4. Keep descriptions concise and helpful
5. Organize tools by category if helpful

Run `--help` or `--version` on any tool to verify it's installed and learn its syntax.

## Essential Tools

These are commonly used tools that many developers have installed:

- git: Version control system
- curl: Transfer data from or to a server
- wget: Network downloader
- ssh: Secure shell client for remote access
- rsync: Efficiently transferring and synchronizing files

## Modern CLI Replacements

Enhanced alternatives to traditional Unix tools:

- ripgrep (`rg`): Better file text search (replaces grep)
- fd: A simple, fast and user-friendly alternative to 'find'
- bat: Cat clone with syntax highlighting and Git integration
- lsd or exa: The next gen ls command with colors and icons
- procs: A modern replacement for ps written in Rust
- sd: Intuitive find & replace CLI (sed alternative)
- difft: difftastic - A structural diff that understands syntax

## File and Data Processing

- jq: Command-line JSON processor
- yq: YAML, JSON, XML, CSV, TOML and properties processor
- gron: Make JSON greppable!
- hq: A HTML processor inspired by jq
- pandoc: Swiss-army knife of markup format conversion

### CSV Tools (csvkit)

Suite of command-line tools for working with CSV:

- `csvlook`: Render a CSV file in the console as a Markdown-compatible table
- `csvcut`: Filter and truncate CSV files
- `csvgrep`: Search CSV files
- `csvjoin`: Execute a SQL-like join to merge CSV files
- `csvsort`: Sort CSV files
- `csvstat`: Print descriptive statistics for each column
- `csvjson`: Convert a CSV file into JSON
- `in2csv`: Convert other formats to CSV
- `csvsql`: Generate SQL statements or query CSV directly

## Development Tools

### Code Quality and Linting

- shellcheck: Finds bugs in your shell scripts
- prettier: Code formatter for JavaScript, CSS, JSON, GraphQL, Markdown, YAML
- yamllint: Linter for YAML files
- eslint: JavaScript and TypeScript linter (if using Node.js)
- pylint or ruff: Python linters (if using Python)

### Editors

- vim or neovim: Modal text editor
- nano: Simple text editor
- emacs: Extensible text editor (if preferred)

### Version Control and CI/CD

- gh: GitHub CLI tool
- glab: GitLab CLI tool
- act: Run GitHub Actions locally (optional)

## Infrastructure and DevOps

### Infrastructure as Code

- terraform: Infrastructure provisioning tool
- terraform-docs: Generate documentation from Terraform modules
- tflint: Terraform linter
- ansible: Configuration management and automation
- packer: Machine image builder

### Containers and Kubernetes

- docker: Container platform
- kubectl: Kubernetes command-line tool
- kubectx: Tool to switch between contexts (clusters) on kubectl
- helm: The Kubernetes Package Manager
- k9s: Terminal UI for Kubernetes (optional)

### Security Scanning

- trivy: Scanner for vulnerabilities in container images, file systems, and Git repositories
- checkov: Static code analysis tool for infrastructure-as-code
- snyk: Find and fix vulnerabilities in dependencies (optional)

### Cloud Provider CLIs

- aws-cli: AWS command-line interface
- azure-cli (`az`): Azure command-line interface
- gcloud: Google Cloud SDK command-line interface

## Monitoring and Debugging

- mtr: Combines the functionality of traceroute and ping into one tool
- htop or btop: Interactive process viewer
- lsof: List open files
- netstat or ss: Network statistics
- tcpdump or ngrep: Network packet analyzer

## Productivity Tools

- entr: Run arbitrary commands when files change
- fzf: Command-line fuzzy finder
- tmux: Terminal multiplexer
- zoxide or autojump: Smarter cd command
- glow: Render markdown on the CLI, with pizzazz!

## Performance and Benchmarking

- hyperfine: A command-line benchmarking tool
- ab (Apache Bench): HTTP server benchmarking tool
- wrk or oha: HTTP load generators

## Database Tools

- psql: PostgreSQL interactive terminal
- mysql: MySQL command-line client
- mongosh: MongoDB shell
- redis-cli: Redis command-line interface
- sqlite3: SQLite command-line interface

## Specialized Tools

Add any specialized tools for your specific workflow:

- mise: dev tools, env vars, task runner
- jira-cli: Command line tool for Atlassian Jira
- newrelic-cli: Command line interface for New Relic
- datadog-cli: Datadog command-line interface

## Custom Scripts

Document any custom scripts or tools you've created:

- `my-script`: Description of what it does
- `another-tool`: Description and usage

## Tool Installation

Common package managers for installing these tools:

### macOS

```bash
brew install ripgrep fd bat jq yq
```

### Linux (Ubuntu/Debian)

```bash
apt install ripgrep fd-find bat jq
```

### Linux (Fedora/RHEL)

```bash
dnf install ripgrep fd-find bat jq
```

### Cross-platform

```bash
# Using cargo (Rust package manager)
cargo install ripgrep fd-find bat

# Using npm (Node.js package manager)
npm install -g prettier eslint
```
