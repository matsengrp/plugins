# Matsen Group Claude Code Plugins

A collection of specialized agents for scientific writing, code review, and technical documentation.

## Overview

This plugin collection provides specialized agents designed to enhance your development workflow, particularly for:
- Scientific writing and LaTeX documents
- Code quality and review
- Academic publishing
- Bioinformatics pipelines

## Included Agents

### Scientific Writing & LaTeX
- **scientific-tex-editor** - Expert scientific editing for LaTeX documents following best practices
- **tex-grammar-checker** - Meticulous grammar checking for LaTeX/TeX files
- **tex-verb-tense-checker** - Review LaTeX documents for verb tense consistency
- **topic-sentence-stickler** - Ensure strong topic sentences in paragraph structure
- **pdf-proof-reader** - Proofread PDF proofs from academic journals
- **journal-submission-checker** - Verify repositories, references, and bibliographic information

### Code Quality & Review
- **clean-code-reviewer** - Expert code review focused on clean code principles
- **code-smell-detector** - Gentle code smell detection with mentoring approach
- **antipattern-scanner** - Scan for architectural antipatterns and violations

### Specialized Tools
- **snakemake-pipeline-expert** - Expert guidance on Snakemake workflows
- **math-pr-summarizer** - Create mathematical summaries of statistical/computational PRs
- **pdf-question-answerer** - Analyze and answer questions about scientific PDFs

## Slash Commands

### /pre-pr-check
Comprehensive pre-PR quality checklist that guides you through:
- Issue compliance verification
- Code formatting and documentation checks
- Architecture review with antipattern-scanner and clean-code-reviewer agents
- Test quality validation (no fake tests allowed!)
- Static analysis (ruff, mypy, test coverage)

Run before creating any pull request to ensure code quality standards are met.

## Hooks

### Desktop Notifications (macOS)
Get native macOS notifications when Claude needs your input or completes tasks.

**Prerequisites:**
```bash
brew install terminal-notifier
```

**Included notifications:**
- 🔔 When Claude needs your input
- ✅ When a task is completed

Notifications are automatically enabled when you install the plugin (if `terminal-notifier` is available).

## Installation

### From GitHub
```bash
/plugin add https://github.com/matsengrp/plugins
```

### Local Development
```bash
cd /Users/matsen/re/plugins
/plugin add .
```

## Usage

### Agents
These agents will be available as specialized subagents that Claude Code can invoke automatically based on your task context, or you can invoke them manually using the Task tool.

### Slash Commands
Use slash commands directly in your conversation:
- `/pre-pr-check` - Run comprehensive pre-PR quality checklist

## Structure

```
plugins/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── agents/                   # Agent definitions
├── commands/                 # Custom slash commands
│   └── pre-pr-check.md      # Pre-PR quality checklist
├── hooks/                    # Event handlers
│   └── hooks.json           # Desktop notifications (terminal-notifier)
└── skills/                   # Agent skills (future)
```

## Development

This plugin is designed to replace the legacy `claude-code-agents` repository with the new Claude Code plugin system.

## License

MIT

## Author

Erick Matsen & Matsen Group
