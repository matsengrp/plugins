# Quick Start Guide

## Prerequisites

### Optional: Desktop Notifications (macOS)
To enable desktop notifications when Claude needs input or completes tasks:

```bash
brew install terminal-notifier
```

Test it works:
```bash
terminal-notifier -title "Test" -message "Notifications working!"
```

If you skip this, the plugin will still work but notifications will be silently ignored.

## Testing Your Plugin Locally

1. **Install the plugin locally:**
   ```bash
   cd /Users/matsen/re/plugins
   /plugin add .
   ```

2. **List installed plugins:**
   ```bash
   /plugin list
   ```

3. **Test an agent:**
   Create a test file and ask Claude to use one of the agents. For example:
   ```bash
   # For testing the scientific-tex-editor:
   echo "This is a test LaTeX document with some issues." > test.tex
   # Then ask Claude: "Can you review this tex file with the scientific-tex-editor?"
   ```

4. **Enable/disable the plugin:**
   ```bash
   /plugin disable matsengrp-agents
   /plugin enable matsengrp-agents
   ```

## Publishing to GitHub

1. **Initialize git repository:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Matsen Group Claude Code plugin"
   ```

2. **Create GitHub repository:**
   - Go to https://github.com/matsengrp
   - Create new repository named `plugins`
   - Don't initialize with README (we already have one)

3. **Push to GitHub:**
   ```bash
   git remote add origin https://github.com/matsengrp/plugins.git
   git branch -M main
   git push -u origin main
   ```

4. **Install from GitHub:**
   ```bash
   /plugin add https://github.com/matsengrp/plugins
   ```

## Adding New Agents

1. **Create new agent file in agents/ directory:**
   ```bash
   # Create a new markdown file
   touch agents/my-new-agent.md
   ```

2. **Write agent definition:**
   - Follow the format of existing agents
   - Include clear description and examples
   - Specify tools the agent can use

3. **Test locally:**
   ```bash
   /plugin reload matsengrp-agents
   ```

4. **Commit and push:**
   ```bash
   git add agents/my-new-agent.md
   git commit -m "Add my-new-agent"
   git push
   ```

## Directory Structure Explained

```
plugins/
├── .claude-plugin/          # Plugin metadata (required)
│   ├── plugin.json          # Plugin manifest
│   └── marketplace.json     # Marketplace configuration
├── agents/                  # Agent definitions
│   └── *.md                 # Each agent is a markdown file
├── commands/                # Custom slash commands
│   └── pre-pr-check.md      # Pre-PR quality checklist
├── hooks/                   # Event handlers
│   └── hooks.json           # Desktop notifications config
├── skills/                  # Future: Reusable skills
├── .gitignore              # Git ignore rules
├── README.md               # Main documentation
└── QUICKSTART.md           # This file
```

## Troubleshooting

### Plugin not loading
```bash
# Run with debug flag
claude --debug

# Check plugin status
/plugin list
```

### Agent not appearing
- Verify agent markdown file is in `agents/` directory
- Check that plugin is enabled: `/plugin list`
- Try reloading: `/plugin reload matsengrp-agents`

### Updates not reflecting
```bash
# Reload the plugin
/plugin reload matsengrp-agents

# Or reinstall
/plugin remove matsengrp-agents
/plugin add https://github.com/matsengrp/plugins
```

### Notifications not working
- Verify `terminal-notifier` is installed: `which terminal-notifier`
- Test manually: `terminal-notifier -title "Test" -message "Hello"`
- Check macOS System Settings > Notifications and ensure notifications are enabled
- Verify hooks are loaded: Look for hook confirmation when plugin loads

## Next Steps

- Add more custom slash commands in `commands/`
- Create reusable skills in `skills/`
- Customize hooks for your workflow
- Share with your team!
