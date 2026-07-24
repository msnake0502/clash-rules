# Repository Guidelines

## Project Structure & Module Organization

This repository is a data-only Clash/Mihomo rule-set project. The `release` branch is the published source for Raw URLs and release assets.

- `mydirect.txt` contains mainland-China direct-domain rules.
- `ai.txt` contains overseas AI service domain rules.
- `app.txt` contains `PROCESS-NAME` rules for AI applications.
- `README.md` documents providers, routing behavior, and usage examples.

Each rule file is UTF-8 YAML with a top-level `payload:` key. There is no application source tree, build output, or test directory.

## Build, Test, and Development Commands

No build step is required. Validate changed files before committing:

```powershell
Get-Content .\ai.txt
```

Confirm each domain file starts with `payload:` and that every entry has the form `  - '+.example.com'`. For `app.txt`, use `  - PROCESS-NAME,Example.exe`. Check for blank lines, duplicates, invalid YAML indentation, and overly broad domains such as `+.google.com` or `+.microsoft.com`.

## Rule Style & Naming Conventions

Use two spaces before every payload item. Quote all domain wildcards, for example `  - '+.chatgpt.com'`; do not quote `PROCESS-NAME` entries. Prefer the smallest official domain suffix that covers the service. Do not add shared cloud, CDN, search, or corporate root domains unless their routing purpose is clear.

Use lowercase filenames with the `.txt` suffix. Keep rules grouped by service where practical, remove exact duplicates, and preserve YAML formatting. Add process aliases only when they are established executable names or mobile package identifiers.

## Testing Guidelines

Review changes as data validation: parse the YAML, verify one rule per line, and test the Raw URL after publishing. Domain providers use `behavior: domain`; `app.txt` uses `behavior: classical`. `PROCESS-NAME` behavior differs by core and operating system, so document platform-specific assumptions in the pull request when adding unfamiliar identifiers.

## Commit & Pull Request Guidelines

Use short imperative commit subjects, following existing history: `Add OpenCode service domains`, `Add AI application process rules`, or `Document Clash rule providers`. Keep each commit focused on one rule set or documentation update.

Pull requests should describe the affected file, list added or removed rules, explain why routing is needed, and include validation results. Link supporting official documentation for unfamiliar services or process names. Do not claim that routing rules prevent account restrictions or bypass service terms.
