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
| `/interview <spec file>` | In-depth interview about a spec to uncover hidden requirements |
| `/ralph-setup <description>` | Setup Ralph workflow: interview, create spec, PRD, and prompt files |

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

### /ralph-setup

```
/ralph-setup <describe what you want to build>
```

Sets up a complete Ralph workflow for autonomous iterative development. Conducts an interview to gather requirements, then generates:
- `.ralph/RALPH-SPEC.md` - Comprehensive project specification
- `.ralph/prd.json` - Prioritized user stories
- `.ralph/RALPH-PROMPT.md` - Loop prompt for autonomous implementation
- `.ralph/progress.txt` - Progress tracking file

After setup, start the loop with `/ralph-loop`.

### /interview

```
/interview SPEC.md
```

Conducts an in-depth interview about a specification file, asking non-obvious questions about:
- Technical implementation details and edge cases
- Architecture tradeoffs and scalability concerns
- UI/UX flows, error states, and accessibility
- Business logic edge cases and assumptions

Continues interviewing until all ambiguities are resolved, then updates the spec file with gathered details.

## Structure

```
.claude/
├── commands/
│   ├── interview.md         # /interview command
│   ├── magicblock.md        # /magicblock command
│   ├── ralph-setup.md       # /ralph-setup command
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
