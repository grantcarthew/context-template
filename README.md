# AI Reference Documentation

A structured system for maintaining local technical documentation as a reference library, optimized for AI coding assistants.

## Overview

This repository provides a structured system for maintaining local copies of frequently referenced technical documentation. By keeping documentation local and properly indexed, AI coding assistants can provide faster, more accurate assistance without relying on web queries or API calls.

### Why Use This?

For AI Agents:

- Fast access to comprehensive documentation without web queries
- Structured indexing (CSV) for efficient navigation
- Consistent, up-to-date reference material
- Reduced token usage through direct file access

For Developers:

- Offline access to critical documentation
- Control over documentation versions
- Customizable to your specific tech stack
- Automated updates via simple scripts

## Features

- Automated Updates: Scripts to keep all documentation repositories current
- CSV Indexing: Efficient navigation system for both humans and AI
- Flexible Structure: Organize documentation by your workflow
- Git-Based: Leverage shallow clones and sparse checkouts to minimize disk usage
- AI Agent Configuration: Customizable ENVIRONMENT.md for AI agent context
- Minimal Dependencies: Only requires Git, Bash 5+, fd, and ripgrep

## Prerequisites

- Git: Version control (2.25+)
- Bash: Shell (5.0+)
- fd: Fast file finder ([installation](https://github.com/sharkdp/fd))
- ripgrep: Fast text search ([installation](https://github.com/BurntSushi/ripgrep))

Optional but recommended:

- lsd or exa: Enhanced directory listings
- bat: Syntax-highlighted file viewing

## Installation

### 1. Clone This Repository

```bash
git clone https://github.com/grantcarthew/reference-template.git ~/reference
cd ~/reference
```

You can fork this repository to track your own customizations.

### 2. Customize Configuration Files

Edit `ENVIRONMENT.md` with your system information:

```bash
vim ~/reference/ENVIRONMENT.md
```

Fill in:

- Your name, skills, and preferences
- Operating system details
- Terminal configuration
- Preferred CLI tools

### 3. Customize Tools List

Edit `docs/tools.md` to reflect your installed tools:

```bash
vim ~/reference/docs/tools.md
```

### 4. Make Scripts Executable

```bash
chmod +x ~/reference/update-references
chmod +x ~/reference/scripts/update-repos
chmod +x ~/reference/scripts/update-docs
```

## Quick Start

### Adding Your First Documentation Repository

1. Choose documentation to clone (see `docs/source.md` for examples):

```bash
cd ~/reference
git clone --depth=1 https://github.com/kubernetes/website.git kubernetes
```

2. Test the update script:

```bash
./update-references
```

3. Configure your AI coding assistant to read:
   - `~/reference/ENVIRONMENT.md` - Your environment configuration
   - `~/reference/AGENTS.md` - Instructions for AI agents
   - `~/reference/ROLE.md` - AI agent role definition

### Example: Adding Multiple Documentation Sources

```bash
cd ~/reference

# Cloud platforms
git clone --depth=1 https://github.com/hashicorp/terraform-docs.git terraform

# Programming languages
git clone --depth=1 https://github.com/golang/go.git golang

# Tools
git clone --depth=1 https://github.com/docker/docs.git docker

# Update all at once
./update-references
```

## Directory Structure

```
~/reference/
├── README.md              # This file - project introduction
├── AGENTS.md              # Instructions for AI agents
├── ROLE.md                # AI agent role definition
├── ENVIRONMENT.md         # Your environment configuration (customize!)
├── PROJECT.md             # Repository maintenance documentation
├── .gitignore             # Excludes child directories and INDEX.csv files
├── update-references      # Main update script
├── docs/                  # Local documentation
│   ├── INDEX.csv          # Index of local docs (gitignored, branch-specific)
│   ├── source.md          # Documentation sources and examples
│   └── tools.md           # CLI tools reference (customize!)
├── scripts/               # Utility scripts
│   ├── lib.sh             # Shared functions for scripts
│   ├── update-repos       # Updates git repositories
│   ├── update-docs        # Downloads web-based docs
│   └── update-docs-url-list.csv  # Web sources configuration
└── [your-docs]/           # Your cloned documentation (gitignored)
    ├── INDEX.csv          # Per-repository index (optional)
    └── ...
```

## Usage

### Updating All Documentation

Run the main update script regularly:

```bash
~/reference/update-references
```

This will:

1. Update all git repositories (shallow pull)
2. Download web-based documentation
3. Report successes and failures

### Searching Documentation

```bash
# Search across all documentation
cd ~/reference
rg -i "search term" --type md

# Search within specific documentation
rg -i "kubernetes pod" kubernetes/

# Find files by name
fd "install.md" ~/reference
```

### Using with AI Coding Assistants

Your AI assistant (like Claude Code) can read:

1. Environment context: `ENVIRONMENT.md`
2. Agent instructions: `AGENTS.md` and `ROLE.md`
3. Documentation indexes: `INDEX.csv` files for quick navigation
4. Direct documentation access: Any file in cloned repositories

The AI can efficiently search, navigate, and reference documentation without external API calls.

## Customization

### Branching Strategy

The included `.gitignore` excludes child directories and INDEX.csv files, allowing you to:

- Create different branches for different contexts (work, personal, projects)
- Maintain different documentation sets per branch
- Keep the core files synchronized across branches

### Creating Custom INDEX.csv Files

For large documentation repositories, create an INDEX.csv file:

```csv
directory,section,description,file_path,topics
docs,getting-started,Installation and setup,docs/install.md,setup;installation
docs,api,API reference,docs/api/README.md,api;reference
```

See `AGENTS.md` for detailed indexing guidelines.

### Adding Web-Based Documentation

Edit `scripts/update-docs-url-list.csv`:

```csv
url,filename,description
https://example.com/docs,example-docs.md,Example Documentation
```

Note: Requires a web-to-markdown converter tool.

## Maintenance

### Regular Updates

Set up a weekly update routine:

```bash
# Add to crontab or run manually
cd ~/reference && ./update-references
```

### Troubleshooting

Script fails to find lib.sh:

- Ensure scripts are run from the repository root or have correct paths

Git repositories fail to update:

- Check network connectivity
- Verify repository URLs are still valid
- See `docs/source.md` troubleshooting section

Disk space issues:

- Use shallow clones (`--depth=1`)
- Use sparse checkouts for large repositories
- Remove unused documentation repositories

## Contributing

Contributions are welcome! If you have improvements to this repository:

1. Fork this repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

Please ensure:

- Scripts remain POSIX-compliant where possible
- Documentation is clear and concise
- Changes benefit the general use case

## License

Mozilla Public License Version 2.0

## Acknowledgments

This repository is designed to work seamlessly with:

- AI coding assistants
- Modern CLI tools (ripgrep, fd, bat, etc.)
- Git-based documentation workflows

## Resources

- Documentation Sources: See `docs/source.md` for curated examples
- CLI Tools: See `docs/tools.md` for recommended tools
- Agent Instructions: See `AGENTS.md` for AI agent integration details
- Role Definition: See `ROLE.md` for AI agent role and responsibilities
