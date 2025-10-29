# Reference Repository Refresh

## Project Overview

This project maintains the reference repository's INDEX.csv file system. The repository contains Git-cloned documentation sources, tool/application source code, and local documentation directories that serve as reference material. Each source should have a child INDEX.csv file that catalogs its contents in a format appropriate to that source. The root INDEX.csv provides a master inventory of all child directories.

Project Type: Repository maintenance and indexing

Status: Recurring maintenance task

Critical Constraints:

- Read-only/Create/Update operations only - NEVER delete files
- Root INDEX.csv contains child directories only - NEVER include root-level files

## Goals

1. Discover all content sources - Find all git repositories and significant local directories
2. Validate child INDEX.csv files - Ensure each source has an appropriate INDEX.csv
3. Create missing child INDEX.csv files - Generate new indexes with schemas suited to each source's structure
4. Update existing child INDEX.csv files - Refresh outdated entries, add missing content
5. Synchronize root INDEX.csv - Update master inventory to reflect current state

## Scope

### In Scope

- Discovery of all git repositories and significant local directories from the reference directory root
- Analysis of documentation and source code structure within each source
- Creation/update of child INDEX.csv files with appropriate schemas for each source type
- Update of root INDEX.csv to reflect all child directories only (NOT root-level documents)
- Validation of existing INDEX.csv entries against actual directory contents
- Topic taxonomy updates
- Last updated date synchronization

CRITICAL: Root INDEX.csv entries must be child directories only. Never include root-level markdown files (ENVIRONMENT.md, PROJECT.md, README.md, ROLE.md, etc.) in the root INDEX.csv.

### Out of Scope

- Modification of content within git repositories
- Git operations (pull, commit, push) on cloned repositories
- Creation of new documentation sources
- Removal of existing documentation sources
- Changes to repository structure or organization
- Automated scheduling of refresh tasks
- Changes to PROJECT.md and AGENTS.md documents

CRITICAL CONSTRAINT: This project MUST NEVER delete or remove any files. All operations are read-only or create/update only. If files are discovered that seem out of place, document them but do not delete them.

## Technical Approach

### Discovery Phase

1. Find all git repositories and significant local directories

   - Git repositories: `fd --type d --hidden --no-ignore --min-depth 2 '^\.git$' .`
   - Local directories: Identify directories with substantial content (e.g., `docs/`) `lsd --tree --depth 1`
   - Exclude: Utility directories like `scripts/`
   - Identify type (documentation, source code, tools, local docs)

2. Catalog existing INDEX.csv files

   - Root level INDEX.csv
   - All child INDEX.csv files
   - Use `fd --type f --hidden --no-ignore 'INDEX.csv'`

3. Compare discoveries against root INDEX.csv

   - Identify missing entries
   - Identify orphaned entries

### Child INDEX.csv Management

For each source (git repository or local directory):

1. Analyze structure

   - Identify primary content paths
   - Determine type: documentation, source code, tools, or local docs
   - Identify logical categories/sections

2. Design appropriate schema

   - Each source may have a different CSV schema
   - Schema should reflect the source's organization
   - Common patterns:
     - Documentation: `directory,section,description,file_path,topics`
     - Source code: `directory,component,description,path,language`
     - Tools: `directory,area,description,path,topics`
     - Local docs: `directory,file,description,topics`
   - Use whatever column structure best represents the content
   - Avoid any date last updated type fields, these are in the root INDEX.csv file
   - Avoid count fields to reduce unnecessary update churn

3. Determine what to index (token efficiency principle)

   - Include: Content that helps LLMs understand how to USE the tool/library
     - READMEs and main documentation
     - API documentation and guides
     - Key source code directories that implement main features
     - Configuration examples
   - Exclude: Content relevant only to contributors/developers
     - Contributing guides (CONTRIBUTING.md)
     - Code of conduct files
     - CI/CD configurations
     - Test infrastructure and mocks
     - Internal utilities and helpers
     - Development tooling
   - Goal: Minimize token usage while maximizing reference value

4. Generate/update INDEX.csv

   - Create or update with appropriate schema
   - Extract metadata from README, directory names, or file headers
   - Use relative paths from source root
   - Index only high-value reference content

### Root INDEX.csv Update

IMPORTANT: The root INDEX.csv MUST only contain child directories, NOT root-level documents. Do not include ENVIRONMENT.md, PROJECT.md, README.md, ROLE.md, or any other root-level files in the root INDEX.csv.

1. Read current root INDEX.csv
2. Validate each entry against filesystem
3. Add new entries for discovered child directories only (repositories and local directories like docs/)
4. Exclude all root-level files from the root INDEX.csv
5. Update fields:
   - `last_updated`: Current date (YYYY-MM-DD)
   - `topics`: Synchronized with content
6. Write updated root INDEX.csv

### Validation

1. Verify CSV integrity
2. Test that paths in INDEX.csv files are valid
3. Cross-reference root and child indexes
4. Document any anomalies

## Success Criteria

- All git repositories and significant local directories discovered and catalogued
- Each source has an appropriate child INDEX.csv (schema fits the content)
- Root INDEX.csv accurately reflects all child directories (NOT root-level files)
- All INDEX.csv files are valid CSV format
- Last updated dates reflect refresh date (only root level INDEX.csv)
- Topics are meaningful and well-organized
- NO FILES DELETED - All operations are non-destructive

## Implementation Notes

### Source Types

This reference directory may contain:

- Documentation repositories: Official docs cloned for reference (git)
- Tool/application source code: Useful reference implementations (git)
- Library source code: Examples and API references (git)
- Configuration repositories: Reference configurations (git)
- Local documentation directories: Maintained markdown files (local, e.g., `docs/`)

Each type may benefit from a different INDEX.csv schema. Note that `scripts/` and similar utility directories should be excluded from indexing.

### Date Format

Always use ISO 8601 format: `YYYY-MM-DD`

### Topic Taxonomy

- Use lowercase
- Use hyphens for multi-word topics (e.g., `ci-cd`)
- Separate with semicolons
- 3-7 topics per entry typically

### Path References

- Always use relative paths
- Relative to source root (repository or directory) for child INDEX.csv
- Relative to reference directory root for root INDEX.csv

### Root INDEX.csv Scope

CRITICAL RULE: The root INDEX.csv file catalogs ONLY child directories (subdirectories within ~/reference/), NOT root-level files.

Include:

- Child directories like: docs/, gitlab/, golang/, etc
- Both git repositories and local directories

Exclude:

- All root-level markdown files: ENVIRONMENT.md, PROJECT.md, AGENTS.md, README.md, ROLE.md
- The scripts directory
- Script files: update-docs, update-repos, update-references
- Hidden files and directories: .git, .gitignore

Root-level documentation files are important but should NOT appear in the root INDEX.csv. They are discovered and read directly by AI agents as part of session initialization.

## Related Documentation

- [AGENTS.md](AGENTS.md) - AI agent context for reference repository
- [README.md](README.md) - Human-readable repository overview
- [ROLE.md](ROLE.md) - AI agent role definition
- [ENVIRONMENT.md](ENVIRONMENT.md) - User and system environment configuration
- [docs/source.md](docs/source.md) - External documentation sources and setup
