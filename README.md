░░ ░▒▓█  ░░ ░▒▓█  ░░ ░▒▓█ ░░ ░▒▓█  ░░ ░▒▓█  ░░ ░▒▓█ ░░ ░▒▓█  ░░ ░▒▓█  ░░ ░▒▓█ ░░ ░
░▒  ░▒▓ ░
░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒▓  ░▒ ░▒
░▒▓█ ░░  ░▒▓█ ░░  ░▒▓█ ░░ ░▒▓█ ░░  ░▒▓█ ░░  ░▒▓█ ░░ ░▒▓█ ░░  ░▒▓█ ░░  ░▒▓█ ░░ ░▒▓█ ░░


# slow-coder

A skill for AI coding agents that shifts the model from **driver** to **navigator**.

You work out each step together. Once the next small slice is clear, the AI can
help write bounded code without outrunning your understanding.

> "You can vibe code. But you can't vibe understanding."

Read the [philosophy](skills/slow-coder/philosophy.md) behind this approach.

---

## The Problem

AI agents give you high leverage — but high leverage without visibility means
you're shipping code you don't understand. Slow Coder targets the sweet spot:
**high leverage AND high visibility**.

Instead of dumping whole files or projects, the AI reads the codebase, breaks
the problem into steps, explains the why, helps with syntax, writes only the
agreed slice when asked, and reviews the result with you. You stay in the
driver's seat.

---

## Install

Choose the install path that matches your agent. Like
[`caveman`](https://github.com/JuliusBrussee/caveman), Slow Coder keeps a
canonical skill in `skills/slow-coder/SKILL.md` and exposes agent-specific
adapters for tools that do not consume skills directly.

The `skills` CLI and Claude Code plugin paths do not require cloning this
repository. The manual copy paths assume you have cloned the repo and are
running commands from its root:

```bash
git clone https://github.com/w-v-r/slow-coder.git
cd slow-coder
```

### Claude Code

#### Quick Install

Install the Claude Code plugin with the Slow Coder banner:

```bash
curl -fsSL https://raw.githubusercontent.com/w-v-r/slow-coder/main/install.sh | sh
```

Verify it in any Claude Code session:

```
/slow-coder
```

#### Skills CLI

Install the skill directly with the [`skills`](https://skills.sh/docs) CLI:

```bash
npx skills add w-v-r/slow-coder --global --agent claude-code --skill slow-coder -y
```

Verify it in Claude Code:

```
/slow-coder
```

#### Plugin

Add the marketplace and install the plugin:

```bash
claude plugin marketplace add w-v-r/slow-coder
claude plugin install slow-coder
```

Verify it in any Claude Code session:

```
/slow-coder
```

#### Manual Skill Install

From a clone of this repository, copy the skill directly without the plugin
system:

```bash
mkdir -p ~/.claude/skills/slow-coder
cp skills/slow-coder/SKILL.md ~/.claude/skills/slow-coder/SKILL.md
cp skills/slow-coder/philosophy.md ~/.claude/skills/slow-coder/philosophy.md
```

Then verify with `/slow-coder` in Claude Code.

### Cursor

Install the skill directly with the [`skills`](https://skills.sh/docs) CLI:

```bash
npx skills add w-v-r/slow-coder --global --agent cursor --skill slow-coder -y
```

Verify it by opening Cursor chat and invoking Slow Coder:

```
@slow-coder
```

#### Manual Rule Install

For global use across all projects, copy the Cursor rule to your user rules:

```bash
mkdir -p ~/.cursor/rules
cp adapters/cursor/slow-coder.mdc ~/.cursor/rules/slow-coder.mdc
```

For one project only, copy it into that project's `.cursor/rules` directory:

```bash
mkdir -p .cursor/rules
cp adapters/cursor/slow-coder.mdc .cursor/rules/slow-coder.mdc
```

Verify it by opening Cursor chat and @mentioning the rule:

```
@slow-coder
```

### GitHub Copilot

Copy the instructions to the project where you want Slow Coder behavior:

```bash
mkdir -p .github
cp adapters/copilot/copilot-instructions.md .github/copilot-instructions.md
```

Copilot will apply slow-coder mode for all interactions in that project.

> Note: `copilot-instructions.md` is always-on within a project. Use it on
> projects where you want slow-coder mode by default, not as a toggle.

### Other Agents (OpenAI Codex, Amp, etc.)

For agents that read `AGENTS.md` from the project root, copy the generic
adapter:

```bash
cp adapters/generic/AGENTS.md ./AGENTS.md
```

Verify by starting your agent in that project and asking it to enter Slow Coder
mode.

---

## Usage

Once activated, the agent will:

1. **Gather context** — read the relevant files and understand the problem
2. **Plan together** — propose a numbered step-by-step breakdown
3. **Confirm the next slice** — agree on behavior, API, types, tests, or acceptance criteria
4. **Guide implementation** — help with syntax, let you write it, or apply the bounded agreed edit
5. **Review** — check the result with you before moving on
6. **Reflect** — summarize what was built, check your understanding

The agent can help write small, local changes once you have agreed on the
specific step. It should not pump out whole files, whole components, broad
multi-file scaffolds, or complete projects while Slow Coder mode is active.

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
│   ├── marketplace.json               # Claude Code marketplace metadata
│   └── plugin.json                    # Claude Code plugin metadata
├── .cursor/
│   ├── rules/
│   │   └── slow-coder.mdc             # Repo-local Cursor rule
│   └── skills/
│       └── slow-coder/
│           ├── SKILL.md               # Repo-local Cursor skill copy
│           └── philosophy.md          # Referenced by the Cursor skill copy
├── skills/
│   └── slow-coder/
│       ├── SKILL.md                   # Canonical skill definition
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
