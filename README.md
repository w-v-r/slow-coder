# slow-coder

A skill for AI coding agents that shifts the model from **driver** to **navigator**.

You write the code. The AI handles context, explanation, and review.

> "You can vibe code. But you can't vibe understanding."

Read the [philosophy](skills/slow-coder/philosophy.md) behind this approach.

---

## The Problem

AI agents give you high leverage — but high leverage without visibility means
you're shipping code you don't understand. Slow Coder targets the sweet spot:
**high leverage AND high visibility**.

Instead of generating code for you, the AI reads the codebase, breaks the
problem into steps, explains the why, reviews what you write, and asks
questions to keep you thinking. You stay in the driver's seat.

---

## Install

### Claude Code

Add the marketplace and install:

```bash
claude plugin marketplace add w-v-r/slow-coder
claude plugin install slow-coder
```

Then invoke it in any session:

```
/slow-coder
```

Or install the skill directly without the plugin system:

```bash
mkdir -p ~/.claude/skills/slow-coder
cp skills/slow-coder/SKILL.md ~/.claude/skills/slow-coder/SKILL.md
cp skills/slow-coder/philosophy.md ~/.claude/skills/slow-coder/philosophy.md
```

### Cursor

Copy the rule to your global Cursor rules (applies across all projects):

```bash
mkdir -p ~/.cursor/rules
cp adapters/cursor/slow-coder.mdc ~/.cursor/rules/slow-coder.mdc
```

Or add to a specific project only:

```bash
mkdir -p .cursor/rules
cp adapters/cursor/slow-coder.mdc .cursor/rules/slow-coder.mdc
```

Activate it by @mentioning the rule in Cursor chat: `@slow-coder`

### GitHub Copilot

Copy the instructions to your project:

```bash
mkdir -p .github
cp adapters/copilot/copilot-instructions.md .github/copilot-instructions.md
```

Copilot will apply slow-coder mode for all interactions in that project.

> Note: `copilot-instructions.md` is always-on within a project. Use it on
> projects where you want slow-coder mode by default, not as a toggle.

### Other Agents (OpenAI Codex, Amp, etc.)

For agents that read `AGENTS.md` from the project root:

```bash
cp adapters/generic/AGENTS.md ./AGENTS.md
```

---

## Usage

Once activated, the agent will:

1. **Gather context** — read the relevant files and understand the problem
2. **Plan together** — propose a numbered step-by-step breakdown
3. **Guide implementation** — explain each step, ask what you think, wait for you to write it, then review
4. **Reflect** — summarize what was built, check your understanding

The agent will not write code to files. It will ask questions, show short
in-chat snippets as hints, and review everything you write.

### When to use it

- Learning something new by implementing it
- Code you'll need to maintain, debug, and extend
- Complex algorithms where understanding the details matters
- Refactoring — when you need to understand what exists before changing it

### When not to use it

- Boilerplate and scaffolding
- Configuration files
- Patterns you've implemented many times and fully understand
- Tight deadlines where speed genuinely matters more than understanding

---

## File Structure

```
slow-coder/
├── .claude-plugin/
│   └── plugin.json                    # Claude Code plugin metadata
├── skills/
│   └── slow-coder/
│       ├── SKILL.md                   # Claude Code skill definition
│       └── philosophy.md              # The why behind slow-coder
├── adapters/
│   ├── cursor/
│   │   └── slow-coder.mdc             # Cursor rules adapter
│   ├── copilot/
│   │   └── copilot-instructions.md    # GitHub Copilot adapter
│   └── generic/
│       └── AGENTS.md                  # Generic AGENTS.md adapter
├── LICENSE
└── README.md
```

---

## License

MIT
