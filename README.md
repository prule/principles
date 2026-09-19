# Project Principles

A constitution for agents building software in this project. These rules govern design decisions. When a task conflicts with a principle, say so before proceeding.

Read the individual file when a decision turns on that principle. The one-liners below are the working summary.

| Principle | Rule |
|---|---|
| [SOLID](solid.md) | Five OO design rules; the umbrella for SRP, Open/Closed, and Dependency Inversion. |
| [DRY](dry.md) | One authoritative home per piece of knowledge — but duplication beats a wrong abstraction. |
| [KISS](kiss.md) | The simplest thing that fully solves the stated problem. |
| [YAGNI](yagni.md) | Build what is asked for now; no speculative features. |
| [SRP](srp.md) | One reason to change per unit. |
| [Open/Closed](open-closed.md) | Add behaviour by adding code, not editing working code. |
| [Dependency Inversion](dependency-inversion.md) | Depend on abstractions; inject dependencies; wire at the edge. |
| [Composition](composition.md) | Assemble small parts; inheritance only for true "is-a". |
| [Separation of Concerns](separation-of-concerns.md) | Layer the system; dependencies point inward. |
| [Fail Fast](fail-fast.md) | Surface problems early and loudly; never swallow errors. |
| [Measure First](measure-first.md) | No optimisation without a number, before and after. |
| [Least Privilege](least-privilege.md) | Minimum access, minimum scope, minimum lifetime. Default deny. |

## Patterns

[patterns/](patterns/README.md) documents the architectural and code-level patterns used here — DDD, hexagonal architecture, testing strategy, and the distributed-systems set.

The distinction matters: **principles always apply; patterns apply only when the problem has the shape they solve.** Reaching for a pattern the problem does not call for violates KISS and YAGNI. Each pattern file says when not to use it.

## Resolving conflicts

These principles pull against each other. Precedence when they clash:

1. **Least Privilege** and **Fail Fast** — correctness and security are not traded away.
2. **YAGNI** and **KISS** — do not build the abstraction yet.
3. **DRY**, **Open/Closed**, and the rest — apply once the pattern is proven, typically at the third occurrence.

In short: keep it safe, keep it small, and generalise only when reality forces you to.
