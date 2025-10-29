# AI Reference Documentation

A structured system for maintaining local technical documentation as a reference library, optimised for AI coding assistants.

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
- Minimal Dependencies: Only requires Git, Bash 5+, fd, ripgrep, and snag

## Prerequisites

- Git: Version control (2.25+)
- Bash: Shell (5.0+)
- fd: Fast file finder ([installation](https://github.com/sharkdp/fd))
- ripgrep: Fast text search ([installation](https://github.com/BurntSushi/ripgrep))

Optional but recommended:

- snag: Fetch web page content using a browser engine ([installation](https://github.com/grantcarthew/snag))
- kagi: Query the Kagi search engine FastGPT API ([Bash script, not easy to setup, make it your own](https://github.com/grantcarthew/scripts/blob/main/kagi))
- lsd: Enhanced directory listings

## Installation

### 1. Clone This Repository

It's recommended to clone this repository into your $HOME at ~/reference. This path is used throughout the documents and will need changing if you decide to use a different location.

```bash
git clone https://github.com/grantcarthew/reference-template.git ~/reference
cd ~/reference
```

You can fork this repository to track your own customisations.

### 2. Customise Configuration Files

Edit `ENVIRONMENT.md` and customise this file to make it your own. This is how you tell the AI Agent who you are and where it is.

```bash
nvim ~/reference/ENVIRONMENT.md
```

Fill in:

- Your name, skills, and preferences
- Desktop environment and package manager details

Add or remove anything so your AI Agent can be fun and work effectively.

### 3. Make Scripts Executable

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

_Note: You don't want to clone the whole of the internet here, just reference documentation you use all the time._

2. Test the update script:

```bash
./update-references
```

3. Configure your AI coding assistant to read the following files during every session start:

- `~/reference/ENVIRONMENT.md` - Your environment configuration
- `~/reference/INDEX.csv` - Your reference index

_Note: You should also be reading the local directory AGENTS.md (not this one) and setting a role._

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
├── README.md                     # This file - project introduction
├── AGENTS.md                     # Instructions for AI agents
├── ROLE.md                       # AI agent role definition
├── ENVIRONMENT.md                # Your environment configuration (customise!)
├── PROJECT.md                    # Repository maintenance documentation
├── .gitignore                    # Excludes child directories and INDEX.csv files
├── update-references             # Main update script
├── docs/                         # Local documentation
│   ├── INDEX.csv                 # Index of local docs (gitignored, branch-specific)
│   └── source.md                 # Documentation sources and examples
├── scripts/                      # Utility scripts
│   ├── lib.sh                    # Shared functions for scripts
│   ├── update-repos              # Updates git repositories
│   ├── update-docs               # Downloads web-based docs
│   └── update-docs-url-list.csv  # Web sources configuration
└── [your-docs]/                  # Your cloned documentation (gitignored)
    ├── INDEX.csv                 # Per-repository index (optional)
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

1. Environment context: `~/reference/ENVIRONMENT.md`
2. Documentation indexe: `~/reference/INDEX.csv` file for quick navigation
3. Agent local instructions: `AGENTS.md` and `ROLE.md`
4. Project or plan files: `PROJECT.md` file for current scope of work or tasks
5. Direct documentation access: Any file in cloned repositories

The AI can efficiently search, navigate, and reference documentation without external API calls.

Prompt example:

_Note: You should automate this as I've done here [start](https://github.com/grantcarthew/scripts/blob/main/start)_

```txt
Read the ~/reference/ENVIRONMENT.md file for environment context. Read the ~/reference/INDEX.csv
for documentation context. Read the AGENTS.md file for repository context.
Read the PROJECT.md document. Respond with the project title, and the shortest possible summary
of work required. Include completed tasks. Number the items for ease of reference.
```

Once the AI Agent has finished reading the documents, during a session if you need it to skill up on a cloned repo and it doesn't do it itself, motivate it with:

```txt
Please read the GitLab pipeline documentation before we start.
```

I'm using GitLab as an example here. The AI Agent will immediately read from the known INDEX.csv files.

In the above example, the ENVIRONMENT.md and INDEX.csv files are the home reference resources, the AGENTS.md and PROJECT.md documents are local repository files. Don't use the AGENTS.md and PROJECT.md documents in this repository, they are for working on the reference repository itself.

Read more about [AGENTS.md](https://agents.md) and have a look at the local [PROJECT.md](PROJECT.md) document as a project example.

More project examples can be found in the [snag project](https://github.com/grantcarthew/snag/tree/main/docs/archive).

## Customisation

### Branching Strategy

The included `.gitignore` excludes child directories and INDEX.csv files, allowing you to:

- Create different branches for different contexts (work, personal, projects)
- Maintain different documentation sets per branch
- Keep the core files synchronised across branches

### Creating INDEX.csv Files

In the age of AI Agents, you don't do this yourself.

Launch your AI Agent while in the ~/reference directory, then paste in this prompt:

```txt
Read the ~/reference/ENVIRONMENT.md file for environment context.\
Read the ~/reference/INDEX.csv for documentation context.
Read the AGENTS.md file for repository context.
Read the PROJECT.md document to understand your task.
Once you're read these documents, start the Reference Repository Refresh project work.
```

_Note: Again, you should automate this as I've done here [start](https://github.com/grantcarthew/scripts/blob/main/start)_

### Adding Web-Based Documentation

Edit `scripts/update-docs-url-list.csv`:

```csv
url,filename,description
https://example.com/docs,example-docs.md,Example Documentation
```

_Note: Requires [snag](https://github.com/grantcarthew/snag/tree/main) or similar._

Execute the [update-references](update-references) script.

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

- Scripts support Bash
- Documentation is clear and concise
- Changes benefit the general use case

## License

Mozilla Public License Version 2.0

## Resources

- Documentation Sources: See `docs/source.md` for curated examples
- Agent Instructions: See `AGENTS.md` for AI agent integration details
- Role Definition: See `ROLE.md` for AI agent role and responsibilities
- Project Definition: See `PROJECT.md` for reference repository refresh work
