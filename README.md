# Claude Code Skills

A collection of custom slash commands for [Claude Code](https://claude.ai/code).

## Installation

```bash
git clone https://github.com/sporicle/claude.git /tmp/claude-skills
cp -r /tmp/claude-skills/.claude/commands ~/.claude/
rm -rf /tmp/claude-skills
```

This merges the commands into your existing `~/.claude` directory, making them available in all projects.

## Available Commands

| Command | Description |
|---------|-------------|
| `/magicblock <task>` | MagicBlock Ephemeral Rollups patterns for Anchor/Solana programs |

## Usage

```
/magicblock <describe what you want to do>
```

### Examples

```
/magicblock add delegation hooks to my player account
```

```
/magicblock change my roll_dice function to use VRF
```

```
/magicblock set up a crank that updates game state every 100ms
```

```
/magicblock add dual connection support to my frontend
```

## Structure

```
.claude/
└── commands/
    └── magicblock.md    # /magicblock command
```

## License

MIT
