# Coordinator Pattern — Orchestrating Agent Work

A trusted coordinator manages task decomposition and delegates to specialized agents.

## The Pattern

One "mayor" or "coordinator" agent:
- Receives high-level requests
- Decomposes into subtasks
- Spawns/delegates to worker agents
- Aggregates results
- Maintains overall context

Workers (polecats) handle specific tasks and report back.

## Why It Works

**Separation of concerns:**
- Coordinator: planning, context, user interaction
- Workers: execution, specialized capabilities

**Trust hierarchy:**
- Coordinator is trusted (runs with user's authority)
- Workers are constrained (minimal capabilities)

## Implementation Sketch

```
User Request
     │
     ▼
┌─────────────┐
│ Coordinator │ ← Trusted, maintains context
└─────────────┘
     │
     ├── Task A ──▶ Worker 1 (returns result)
     ├── Task B ──▶ Worker 2 (returns result)
     └── Task C ──▶ Worker 3 (returns result)
     │
     ▼
Synthesized Response
```

## Key Decisions

### What the coordinator keeps:
- User context and preferences
- Task history and state
- Authority to spawn workers
- Final response synthesis

### What workers get:
- Specific, scoped task
- Minimal tools for that task
- No direct user access
- Time/resource bounds

## Communication Patterns

**Request-Response (Simple):**
- Coordinator sends task, waits for result
- Good for sequential, dependent tasks

**Fire-and-Gather (Parallel):**
- Spawn multiple workers simultaneously
- Collect results as they complete
- Good for independent subtasks

**Streaming (Long-running):**
- Workers report progress incrementally
- Coordinator can cancel or redirect
- Good for complex, interruptible work

## Failure Handling

1. **Worker timeout** — Kill and report partial/no result
2. **Worker error** — Log, retry with different approach, or escalate
3. **Coordinator failure** — Harder; needs external supervision

## Security Considerations

- Coordinator is a high-value target (has all context)
- Worker results are untrusted input (validate before using)
- Spawning too many workers = resource exhaustion

## Related

- [Polecat Pattern](polecat.md) — The worker model
- [Human Loop](human-loop.md) — When coordinator needs human input

## Sources

- MapReduce (Dean & Ghemawat, 2004) — Parallel coordination pattern
- Actor model (Hewitt, 1973) — Message-passing concurrency
