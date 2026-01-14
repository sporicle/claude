# Claude Code Skills

A collection of custom slash commands for [Claude Code](https://claude.ai/code).

## Installation

```bash
git clone https://github.com/sporicle/claude.git /tmp/claude-skills
cp -r /tmp/claude-skills/.claude/commands ~/.claude/
cp -r /tmp/claude-skills/.claude/plugins ~/.claude/
rm -rf /tmp/claude-skills
```

This merges the commands and plugins into your existing `~/.claude` directory, making them available in all projects.

## Available Commands

| Command | Description |
|---------|-------------|
| `/magicblock <task>` | MagicBlock Ephemeral Rollups patterns for Anchor/Solana programs |
| `/simplify` | Simplify recently modified code, then commit and push |

## Usage

### /magicblock

```
/magicblock <describe what you want to do>
```

Examples:

```
/magicblock add delegation hooks to my player account
/magicblock change my roll_dice function to use VRF
/magicblock set up a crank that updates game state every 100ms
```

### /simplify

```
/simplify
```

Automatically reviews recently modified files, simplifies the code for clarity and maintainability, runs tests, and commits the changes.

## Structure

```
.claude/
├── commands/
│   ├── magicblock.md        # /magicblock command
│   └── simplify.md          # /simplify command
└── plugins/
    └── code-simplifier/     # Agent for code simplification
        ├── .claude-plugin/
        │   └── plugin.json
        └── agents/
            └── code-simplifier.md
```

## License

MIT
