# Documentation Sources

## Overview

This document provides examples and instructions for cloning external documentation repositories into your reference directory. Customize this file to track your own documentation sources.

## Quick Start

Clone documentation repositories that are relevant to your work. The examples below demonstrate different cloning strategies for various use cases.

## Cloning Strategies

### Standard Shallow Clone

Best for most documentation repositories. Downloads only the latest commit, minimizing disk usage:

```bash
git clone --depth=1 <repository-url> <directory-name>
```

### Sparse Checkout

For large repositories where you only need specific directories:

```bash
git clone --filter=blob:none --sparse <repository-url> <directory-name>
cd <directory-name>
git sparse-checkout set <path-to-docs>
```

### Full Clone

Only when you need complete history or plan to contribute:

```bash
git clone <repository-url> <directory-name>
```

## Example Documentation Sources

Below are examples of useful documentation repositories. Customize this list based on your technology stack and needs.

### Cloud Platforms & Infrastructure

```bash
# AWS Documentation (example - choose relevant services)
git clone --depth=1 https://github.com/awsdocs/aws-documentation.git aws

# Terraform Documentation
git clone --depth=1 https://github.com/hashicorp/terraform-docs.git terraform

# Kubernetes Documentation
git clone --depth=1 https://github.com/kubernetes/website.git kubernetes
```

### Programming Languages & Frameworks

```bash
# Python Documentation
git clone --depth=1 https://github.com/python/cpython.git python/cpython

# Go Documentation
git clone --depth=1 https://github.com/golang/go.git golang

# Node.js Documentation
git clone --depth=1 https://github.com/nodejs/node.git nodejs
```

### Tools & CLI Applications

```bash
# Git Documentation
git clone --depth=1 https://github.com/git/git.git git-scm

# Docker Documentation
git clone --depth=1 https://github.com/docker/docs.git docker
```

## Organizing Your Documentation

### Creating INDEX.csv Files

Each cloned repository should have an `INDEX.csv` file for efficient navigation. The schema can vary based on the source type:

**For documentation repositories**:

```csv
directory,section,description,file_path,topics
docs,getting-started,Quick start guide,docs/getting-started.md,tutorial;setup
```

**For source code repositories**:

```csv
directory,component,description,path,language
src,core,Core library implementation,src/core,go
```

### Directory Structure

Organize repositories logically:

```
~/reference/
├── INDEX.csv           # Master index of all sources
├── docs/               # Local documentation
├── cloud/              # Cloud platform docs
│   ├── aws/
│   └── azure/
├── languages/          # Programming language docs
│   ├── python/
│   └── golang/
└── tools/              # Tool and CLI docs
    ├── docker/
    └── kubernetes/
```

## Recommended Documentation Sources

Choose documentation sources based on your technology stack:

### For DevOps/SRE

- Kubernetes, Docker, Terraform, Ansible, GitLab/GitHub CI/CD
- Cloud provider documentation (AWS, Azure, GCP)
- Monitoring tools (Prometheus, Grafana, New Relic, Datadog)

### For Backend Development

- Language-specific documentation (Python, Go, Java, Node.js)
- Framework documentation (Django, Flask, Express, Spring)
- Database documentation (PostgreSQL, MongoDB, Redis)

### For Frontend Development

- Framework documentation (React, Vue, Angular)
- Build tools (Webpack, Vite, esbuild)
- CSS frameworks (Tailwind, Bootstrap)

### For Data Engineering

- Apache Spark, Airflow, Kafka documentation
- Data warehouse documentation (Snowflake, BigQuery)
- ETL tools and frameworks

## Updating Documentation

The `update-references` script in the repository root automatically updates all cloned repositories:

```bash
~/reference/update-references
```

This script:

- Finds all git repositories in the reference directory
- Performs a shallow pull on each repository
- Reports success, failures, and skipped repositories

## Troubleshooting

### Large Download Size

**Issue**: Clone downloads too much data or takes too long

**Solutions**:

1. **Use shallow clone** for repositories with extensive history:

   ```bash
   git clone --depth=1 <repository-url>
   ```

2. **Use sparse checkout** for large repositories where you only need specific directories:

   ```bash
   git clone --filter=blob:none --sparse <repository-url>
   cd <directory-name>
   git sparse-checkout set <path-to-docs>
   ```

3. **Combine both** for maximum efficiency:
   ```bash
   git clone --depth=1 --filter=blob:none --sparse <repository-url>
   cd <directory-name>
   git sparse-checkout set <path-to-docs>
   ```

### Authentication Issues

**Issue**: Git prompts for credentials or fails to authenticate

**Solutions**:

1. **Use SSH URLs** instead of HTTPS (requires SSH key setup):

   ```bash
   git clone git@github.com:user/repo.git
   ```

2. **Use HTTPS URLs** for public repositories:

   ```bash
   git clone https://github.com/user/repo.git
   ```

3. **Configure Git credentials** for private HTTPS repositories:
   ```bash
   git config --global credential.helper store
   ```

### Update Failures

**Issue**: Repository update fails during `update-references`

**Common causes**:

- Network connectivity issues
- Local uncommitted changes
- Remote branch deleted or renamed
- Merge conflicts

**Solutions**:

1. Check network connectivity
2. Verify repository status: `git status`
3. Reset to remote if needed: `git reset --hard origin/main`
4. Re-clone the repository if persistently problematic

## Tips and Best Practices

1. **Choose relevant sources**: Only clone documentation you regularly reference
2. **Keep it updated**: Run `update-references` weekly or bi-weekly
3. **Create indexes**: Add `INDEX.csv` files to large repositories for easier navigation
4. **Use .gitignore**: The `.gitignore` excludes child directories to keep your repository clean
5. **Document your sources**: Update this file with your cloned repositories and their purposes
