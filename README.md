# Codebase Dump

`codebase-dump.sh` is a simple, efficient Bash script designed to create a single-file text representation of your project. It is specifically optimized for providing full-codebase context to Large Language Models (LLMs).

## Features

- **Smart Filtering:** Automatically respects your `.gitignore` settings.
- **Safety First:** Skips binary files and common lock-files (e.g., `package-lock.json`, `Cargo.lock`, `yarn.lock`).
- **Visual Structure:** Generates a project tree at the beginning of the dump.
- **Flexible Scope:** Supports recursive dumps or top-level-only analysis for both the root and any subfolder.
- **Named Arguments:** Supports short (`-d`, `-R`) and long (`--dir`, `--no-recursive`) flags.
- **Progress Tracking:** Displays real-time status with a file counter.
- **Error Handling:** Exits with a non-zero code and removes the output file if the dump fails or produces an empty result.

## Usage

Ensure the script is executable:
```bash
chmod +x scripts/codebase-dump.sh
```

### Dump the entire project
```bash
bash scripts/codebase-dump.sh
```
Output: `dumps/codebase/codebase-dump.txt`

### Dump a specific subfolder (recursive)
```bash
bash scripts/codebase-dump.sh -d src/components
```
Output: `dumps/codebase/codebase-dump_src_components.txt`

### Dump root-level files only (non-recursive)
```bash
bash scripts/codebase-dump.sh --no-recursive
```
Output: `dumps/codebase/codebase-dump_root-only.txt`

### Dump top-level files of a subfolder only (non-recursive)
```bash
bash scripts/codebase-dump.sh -d src/components --no-recursive
```
Output: `dumps/codebase/codebase-dump_src_components_top-only.txt`

## Requirements

- `bash`
- `git` (the script must be run inside a git repository)
- `perl` (used for robust binary file detection)

## .gitignore recommendation

Add the following to your `.gitignore` to avoid committing dump files:
```
# Dumps (e.g. database dumps, codebase dumps, etc.)
dumps/
```