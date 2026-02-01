# myclaw — Agentic Best Practices Knowledge Base

## What This Is

**This is a knowledge aggregation project, not a code project.**

myclaw ("What Works") distills hard-won lessons from building agentic systems into actionable guidance. Think of it as a field manual for AI agent engineering.

## Structure

```
docs/
├── patterns/        # What works — proven approaches
├── security/        # Threats, mitigations, trust models
├── anti-patterns/   # What doesn't work — failure modes
└── resources/       # Curated external links
```

## How to Read

- **Building an agent?** Start with `patterns/`
- **Security review?** Check `security/` first
- **Learning from others' mistakes?** Browse `anti-patterns/`
- **Going deeper?** Follow links in `resources/`

## Contribution Style

1. **Distill, don't dump** — Extract the insight, not the whole article
2. **Cite sources** — Link to original work, give credit
3. **Be opinionated** — State what works and why; hedging helps no one
4. **Stay practical** — Theory is fine, but show how it applies

## Connection to Sandcastle

This knowledge base informs and is informed by:

- **wasp** — Security whitelist layer for agentic systems
- **propolis** — High-assurance, formally verified agent runtime
- **sandcastle** — The overarching secure agent architecture

Patterns documented here often originate from building these systems. When we learn something the hard way, it goes here so others don't have to.

## Naming

"myclaw" = **My** **C**ollection of **L**essons for **A**gentic **W**ork

(Or just: what I've learned about building agents that actually work.)
