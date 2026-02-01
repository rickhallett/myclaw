# Core Principles

Foundational beliefs that guide agentic system design.

---

## Determinism Over Interpretation

> "These become reproducible, auditable, and don't burn tokens on interpretation. The LLM layer becomes optional — call me for nuance, but the machinery runs without me."
>
> — HAL, on orchestration CLIs (2026-02-01)

**The principle:** Routine operations should be deterministic scripts, not LLM prompts. Reserve AI interpretation for genuinely novel situations.

**Why it matters:**
- **Reproducible** — Same input, same output, every time
- **Auditable** — Clear logs of exactly what happened
- **Cost-efficient** — No tokens burned on routine tasks
- **Reliable** — No hallucination risk for mechanical operations

**Implementation:**
- Build orchestration CLIs (like `bosun`) for recurring workflows
- Use `--dry-run` to preview before executing
- LLM calls become escape hatches, not main paths
- Scripts call other scripts; AI interprets edge cases

**Anti-pattern:** Using an LLM to "figure out" what git commands to run every time you want to push.

---

## Trust Through Transparency

Every action should be previewable before execution. If you can't show what will happen, don't do it.

**Implementation:**
- `--dry-run` flags on all commands
- Clear logging of operations
- Explicit confirmation for destructive actions

---

## Containment by Default

Assume agents will be compromised. Design for blast radius minimization.

**Implementation:**
- Sandboxed execution (polecats)
- Tool restrictions (allowlists, not blocklists)
- Separate contexts for separate trust levels

---

## Memory as Infrastructure

Agents forget between sessions. Memory systems must be:
- Explicit (written, not "remembered")
- Searchable
- Maintainable (consolidation, pruning)
- Secure (private journals, access control)

---

*Add principles as they emerge from practice.*
