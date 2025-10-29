# AGENTS.md

## Repository Overview

This is a local documentation repository that maintains cloned copies of frequently referenced technical documentation. The primary purpose is to provide AI coding agents with fast, efficient access to comprehensive documentation without relying on web queries.

**Key Characteristics**:

- Contains:
  - Git documentation repositories
  - Git source code repositories
  - Local documentation
- Optimized for AI agent consumption
- Maintained via automated update scripts
- Indexed via CSV for quick discovery (INDEX.csv)

## Repository Structure

```txt
~/reference/
├── INDEX.csv           # Branch-specific child directories index (.gitignored)
├── README.md           # Human-readable repository guide
├── ROLE.md             # AI agent role definition
├── AGENTS.md           # This file - AI agent instructions
├── PROJECT.md          # Reference repository maintenance project
├── ENVIRONMENT.md      # User and system environment configuration
├── update-references   # Main update script
├── .gitignore          # Git ignore rules
├── docs/               # Local reference documentation (tracked)
│   ├── INDEX.csv       # Index of reference documentation (.gitignored)
│   ├── source.md       # External documentation sources (synced across branches)
│   └── [doc-file].md   # Other branch-specific local documentation files
├── scripts/            # Utility scripts (synced across branches)
│   ├── update-docs     # Update all git repositories
│   └── update-repos    # Update repository indexes
└── [child-dirs]/       # Branch-specific documentation repositories
    └── INDEX.csv       # Each child has its own INDEX.csv
```

**Note**: The root INDEX.csv and specific child directories vary by branch. Read INDEX.csv to discover available documentation sources for the current branch.

## Adding New Documentation Source

To add a new documentation source:

```bash
cd ~/reference
git clone --depth=1 [repository-url] [directory-name]
```

For sparse checkouts (only specific paths):

```bash
git clone --filter=blob:none --sparse [repository-url] [directory-name]
cd [directory-name]
git sparse-checkout set [path-to-docs]
```

### Update INDEX.csv

After adding a new documentation source, update the INDEX.csv file:

```csv
directory,description,topics,source_url,source_type,last_updated
[dir-name],[description],[topic1;topic2;topic3],[url],[type],[YYYY-MM-DD]
```

**CSV Field Definitions** (for root INDEX.csv):

- `directory`: Name of child directory only - NEVER root-level files
- `description`: Brief description of the documentation content
- `topics`: Semicolon-separated list of main topics covered
- `source_url`: Original URL of documentation source (use N/A for local docs)
- `source_type`: Type of source:
  - `git-sparse-checkout`: Git repo with sparse checkout
  - `official-docs`: Full git clone of official documentation
  - `official-tool-repo`: Git clone of official tool/application repository
  - `local-docs`: Local directory maintained in this repository
- `last_updated`: Date in YYYY-MM-DD format

**CRITICAL**: Root INDEX.csv lists child directories ONLY. Root-level files (ENVIRONMENT.md, PROJECT.md, etc.) are NOT included.

**IMPORTANT**: The root INDEX.csv catalogs ONLY child directories, NOT root-level files. Root-level documentation (ENVIRONMENT.md, PROJECT.md, AGENTS.md, README.md, ROLE.md) is NOT indexed in the root INDEX.csv but is read directly by agents during session initialization. Child directories vary by branch.

Subdirectories have their own INDEX.csv for detailed navigation. Read the root INDEX.csv to discover available child directory indexes for the current branch.

## Maintenance Commands

### Update All Documentation

```bash
~/reference/update-references
```

This script:

- Scans for all Git repositories in the reference directory
- Performs shallow pulls (--depth=1) on each repository
- Updates any copied markdown documents
- Provides a summary of updated, failed, and skipped tasks

### Manual Update of Single Repository

```bash
cd ~/reference/[repo-name]
git pull --depth=1
```

### Check Repository Status

```bash
cd ~/reference/[repo-name]
git status
git log -1
```

## Search and Navigation

### Finding Documentation

**Best Practice for AI Agents**: Read INDEX.csv files directly using the Read tool (most token-efficient approach).

**Quick topic search using Ripgrep on indexes**:

```bash
# Search all INDEX.csv files for a topic
rg -i "[topic]" ~/reference/*/INDEX.csv

# Search main index for keywords
rg "[keyword1]|[keyword2]" ~/reference/INDEX.csv
```

**Full-text search across all documentation**:

```bash
cd ~/reference
rg -i "search-term" --type md
```

**Search within specific documentation source**:

```bash
rg -i "search-term" ~/reference/[directory-name]/
```

**Find files by name pattern**:

```bash
fd --hidden --no-ignore "pattern" ~/reference/
```

**Recommended workflow for agents**:

1. Read `~/reference/INDEX.csv` to identify relevant directory
2. Read the child directory's INDEX.csv for detailed navigation (e.g., `[directory-name]/INDEX.csv`)
3. Navigate directly to the documentation file using the path from the index

## Code Style Guidelines

### Shell Scripts

- Use Bash 5.3.3 syntax
- Include error handling with `set -o pipefail`
- Include usage documentation via `--help` flag
- Use shellcheck for validation

### Markdown Documentation

- Follow CommonMark specification
- Use consistent heading hierarchy
- Include purpose statement at the beginning of each document
- Use relative links for cross-references
- Maintain metadata in frontmatter where applicable

### CSV Files

- Use standard CSV format
- Include header row with clear column names
- Use semicolons for multi-value fields (e.g., topics)
- Use ISO 8601 date format (YYYY-MM-DD)

## File Naming Conventions

- **Root-level metadata**: UPPERCASE (e.g., `README.md`, `AGENTS.md`, `ROLE.md`, `INDEX.csv`)
- **Critical AI configuration**: UPPERCASE (e.g., `ENVIRONMENT.md`)
- **Regular documentation**: lowercase with hyphens (e.g., `github.md`, `source.md`)
- **Scripts**: lowercase, no extension (e.g., `update-docs`)
- **Directories**: lowercase, descriptive names matching source

## Environment Considerations

### Available Tools

Prefer these tools when working with the repository:

- **Ripgrep** (`rg`): Fast text search across files
- **fd**: Modern file finder
- **lsd**: Modern directory listing
- **yq**: YAML/JSON/CSV processor
- **jq**: JSON processor

### Special Considerations

- Git repositories use shallow clones (--depth=1) to minimize disk usage
- Some repositories use sparse checkouts (only specific paths)
- INDEX.csv serves as the single source of truth for documentation sources

## Common Tasks for AI Agents

### Task 1: Find Relevant Documentation

**Example workflow**:

1. Read `~/reference/INDEX.csv` to identify relevant child directory
2. Read `~/reference/[directory-name]/INDEX.csv` for detailed navigation
3. Locate the specific documentation section or file path
4. Navigate directly to the documentation file

**Token optimization**: Reading CSV indexes directly.

### Task 2: Access Environment and Configuration

**Reading user context**:

1. Read `~/reference/ENVIRONMENT.md` for user preferences, OS, tools
2. Read `~/reference/docs/INDEX.csv` to discover available local documentation
3. Read relevant docs files based on current task requirements

### Task 3: Verify Documentation Currency

1. Check `last_updated` field in INDEX.csv
2. Optionally run `update-references` to refresh all sources
3. Verify git log for recent changes: `git log -1 --format="%ai %s"`

### Task 4: Add New Documentation Source

1. Clone repository (standard or sparse checkout as needed)
2. Create directory-level INDEX.csv if documentation is extensive
   - **See PROJECT.md** for indexing philosophy: only include content that helps LLMs understand how to USE the tool
   - Exclude contributor-focused content (CONTRIBUTING, CODE_OF_CONDUCT, CI/CD configs, test infrastructure)
   - Goal: minimize tokens while maximizing reference value
3. Update main INDEX.csv with new entry
4. Test that update-references script works with new repository

### Task 5: Search Across Multiple Sources

1. Use `rg` with appropriate filters:

   ```bash
   rg -i "search-term" --type md ~/reference/
   ```

2. Review results and provide file paths with line numbers
3. Use format: `file_path:line_number` for references

## Security Considerations

- Documentation sources are read-only for AI agents
- Do not modify git histories or commit to documentation repositories

## Troubleshooting

### INDEX.csv Out of Sync

**Symptom**: INDEX.csv doesn't match actual directories

**Resolution**:

1. List actual directories: `lsd --tree --depth <n> ~/reference/`
2. Compare with INDEX.csv entries
3. Update INDEX.csv manually or remove obsolete entries
4. Verify the INDEX.csv file

### Can't Find Expected Documentation

**Symptom**: Search returns no results for known topics

**Resolution**:

1. Check if repository exists: `lsd ~/reference/`
2. Verify INDEX.csv for source information
3. Check if sparse checkout excludes needed paths
4. Run update-references to ensure repositories are current
5. Try broader search terms or different grep patterns

## Related Documentation

### Core Repository Files

- [README.md](README.md) - Human-readable repository overview
- [AGENTS.md](AGENTS.md) - README for AI agents
- [ROLE.md](ROLE.md) - AI agent role definition for documentation architecture
- [INDEX.csv](INDEX.csv) - Master inventory of all documentation sources

### Local Documentation

- [ENVIRONMENT.md](ENVIRONMENT.md) - User and system environment configuration
- [docs/source.md](docs/source.md) - External documentation sources and setup instructions
- [docs/INDEX.csv](docs/INDEX.csv) - Index of local reference documentation (branch-specific)
- Additional docs files vary by branch - see docs/INDEX.csv

### External Documentation Indexes

- Child directory indexes vary by branch - see root INDEX.csv for available sources
