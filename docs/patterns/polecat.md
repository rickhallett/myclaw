# Polecat Pattern — Isolated Agent Instances

Each agent task runs in its own isolated instance with minimal, scoped capabilities.

## The Pattern

Instead of one long-running agent with broad permissions, spawn ephemeral "polecat" instances:

- **Fresh context** — No cross-task contamination
- **Minimal capabilities** — Only tools needed for this specific task
- **Bounded lifetime** — Dies when task completes
- **Auditable** — Clear start/end, single-purpose logs

## Why "Polecat"

Polecats are solitary, focused hunters. Each one handles its own territory. They don't share state or coordinate in packs.

## Implementation

```
Main Agent (Coordinator)
    │
    ├── spawn Polecat A (file operations only)
    ├── spawn Polecat B (web search only)  
    └── spawn Polecat C (code execution, sandboxed)
```

Each polecat:
1. Receives a specific task and limited tool set
2. Executes in isolation
3. Returns results to coordinator
4. Terminates

## Security Benefits

- **Blast radius** — Compromised polecat can't access other tasks' data
- **Privilege separation** — No single instance has all capabilities
- **Audit trail** — Each instance has bounded, traceable actions

## When to Use

- Multi-step tasks with distinct capability needs
- Handling untrusted input (isolate the parser)
- Parallel work that shouldn't share context

## When to Avoid

- Simple, single-tool tasks (overhead not worth it)
- Tasks requiring accumulated context across steps
- Latency-critical paths (spawn time matters)

## Related

- [Coordinator Pattern](coordinator.md) — How the orchestrator manages polecats
- [Trust Boundaries](../security/trust-boundaries.md) — Why isolation matters

## Sources

- Sandcastle architecture documentation
- Principle of least privilege (Saltzer & Schroeder, 1975)
