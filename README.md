# Claude Code Skills

A collection of custom slash commands for [Claude Code](https://claude.ai/code).

## Installation

### Option 1: Clone to your home directory (personal use)

```bash
git clone https://github.com/sporicle/claude.git ~/.claude
```

This makes commands available in all your projects.

### Option 2: Clone to a specific project (team use)

```bash
cd your-project
git clone https://github.com/sporicle/claude.git .claude
```

This makes commands available only in that project and can be shared with your team via version control.

### Option 3: Symlink (if you want to keep the repo elsewhere)

```bash
git clone https://github.com/sporicle/claude.git ~/code/claude-skills
ln -s ~/code/claude-skills/.claude ~/.claude
```

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
