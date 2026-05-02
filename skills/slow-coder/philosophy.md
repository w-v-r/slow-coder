# The Philosophy of Slow Coder

## The Problem

AI coding agents give us extraordinary leverage. They can read entire codebases,
understand complex systems, and produce working code in seconds. This is the
top-right quadrant: **high leverage**.

But high leverage without visibility is dangerous — not because the code is wrong,
but because **you don't understand the code you're shipping**.

The bottom-right quadrant is worse in a different way: full visibility, but you're
back to doing everything yourself. No leverage at all.

Slow coder aims for the sweet spot: **high leverage AND high visibility**.

```
HIGH LEVERAGE
     ↑
     |
     |  Autonomous agents        ← High leverage, low visibility
     |  doing lots of work,        (you don't know what's happening)
     |  but you don't know
     |  what's actually
     |  happening
     |
     +----------------------------→ HIGH VISIBILITY
     |
     |  You see everything,      ← Low leverage, high visibility
     |  but you're back to         (you're doing it yourself)
     |  doing it yourself
     |
LOW LEVERAGE
```

*Framework from [Jacob Deitle](https://www.youtube.com/watch?v=2W5Lew3B1a8)*

---

## No Such Thing as Vibe Understanding

From [Curt Jaimungal](https://curtjaimungal.substack.com/p/why-write):

> You can vibe code. You can vibe art. But you can't vibe your way to understanding.
> You have to work at your understanding.

Getting an LLM to write code for you is the equivalent of getting a machine to lift
weights for you. The machine can aid you, but the growth only happens through your
own effort.

When you produce code via an LLM, you may mistake the LLM's understanding for your
own. The output was always a proxy for understanding. We never fully realized this
until LLMs came along and made it possible to produce fluent, correct output with
minimal input.

**Slow coder exists because understanding requires struggle.**

The model gathers context, explains concepts, reviews your work, and may help
write bounded slices once you understand the shape of the change. But YOU do the
thinking. YOU make the decisions. And through that process, you actually
understand what you've built.

---

## Learning by Coding

There's a powerful way to learn: implement the thing you're studying.

Want to understand a sorting algorithm? Code it.
Want to understand a mathematical concept? Code it.
Want to understand a system design pattern? Code it.

The act of translating an idea into working code forces you to confront every detail.
You can't hand-wave. The compiler doesn't accept vibes. Every edge case, every
type, every conditional — you have to think through it.

This is the mode where slow coder is most valuable. The AI has read the textbook,
the papers, the documentation. It understands the concept deeply. But instead of
dumping a solution, it walks alongside you as you build your own understanding,
one line at a time.

---

## When to Use Slow Coder

- **Learning** — You're studying something and want to learn by implementing it.
- **Important code** — Code that you'll need to maintain, debug, and extend.
- **Complex algorithms** — Where understanding the details matters.
- **Refactoring** — When you need to understand what exists before changing it.
- **Teaching** — When you're pairing with someone and want the AI as a third partner.

## When NOT to Use Slow Coder

- Boilerplate and scaffolding — let the agent handle it.
- Configuration files — no learning value in typing YAML manually.
- Well-understood patterns you've implemented many times before.
- Tight deadlines where speed genuinely matters more than understanding.

Slow coder is a tool, not a religion. Use it when understanding matters.
Use agents when velocity matters. The wisdom is in knowing which moment calls
for which mode.
