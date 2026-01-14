# Claude Code Skills

A collection of custom slash commands for [Claude Code](https://claude.ai/code).

## Installation

### Option 1: Add to your home directory (personal use)

```bash
git clone https://github.com/sporicle/claude.git /tmp/claude-skills
cp -r /tmp/claude-skills/.claude/commands ~/.claude/
rm -rf /tmp/claude-skills
```

This merges the commands into your existing `~/.claude` directory, making them available in all projects.

### Option 2: Add to a specific project (team use)

```bash
cd your-project
mkdir -p .claude/commands
curl -o .claude/commands/magicblock.md https://raw.githubusercontent.com/sporicle/claude/main/.claude/commands/magicblock.md
```

This makes commands available only in that project and can be shared with your team via version control.

## Available Commands

| Command | Description |
|---------|-------------|
| `/magicblock` | MagicBlock Ephemeral Rollups patterns for Anchor/Solana programs |

## Usage

Once installed, open Claude Code and type the command name:

```
/magicblock
```

Claude will load the relevant context and help you with:
- Setting up delegation/undelegation
- Configuring dual connections (base layer + ephemeral rollup)
- Implementing cranks (scheduled tasks)
- Adding VRF (verifiable randomness)
- Best practices and common gotchas

## Structure

```
.claude/
└── commands/
    └── magicblock.md    # /magicblock command
```

## License

MIT
