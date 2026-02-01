# Sandboxing

Isolating agent execution to limit damage from misbehavior or compromise.

## The Principle

Assume agents will eventually do something wrong—through bugs, prompt injection, or unexpected behavior. Sandboxing ensures "wrong" doesn't become "catastrophic."

## Layers of Sandboxing

### Process Isolation
Agent runs in a separate process with limited system access:
- Restricted filesystem (chroot, containers)
- No network or allowlisted endpoints only
- Resource limits (CPU, memory, time)
- Dropped privileges (non-root, capabilities removed)

**Tools:** Docker, Firecracker, gVisor, bubblewrap

### Language-Level
Interpreter/runtime restrictions:
- No `eval()`, `exec()`, or equivalent
- Import restrictions
- Timeouts on execution

**Tools:** RestrictedPython, Deno permissions, WASM sandboxes

### Capability-Based
Agent only has access to explicitly granted tools:
- No ambient authority
- Each capability is a discrete, revocable token
- Principle of least privilege by design

**Tools:** wasp, custom tool registries

### Network Isolation
Control what the agent can reach:
- Allowlist specific domains/IPs
- Block egress except through proxy
- No access to internal services
- DNS filtering

**Tools:** iptables, network namespaces, Cloudflare Gateway

## Implementation Patterns

### Container-per-Task
```
User Request
     │
     ▼
┌─────────────┐
│ Coordinator │
└─────────────┘
     │
     ▼
┌─────────────┐     ┌─────────────┐
│ Container A │     │ Container B │
│ (Task 1)    │     │ (Task 2)    │
│ - fs: /tmp  │     │ - fs: /data │
│ - net: none │     │ - net: api  │
└─────────────┘     └─────────────┘
```

Each task gets fresh, isolated environment.

### Tiered Sandboxes
Different trust levels get different sandboxes:

| Trust Level | Filesystem | Network | Tools |
|-------------|-----------|---------|-------|
| High (system) | Full | Full | All |
| Medium (user) | Home dir | Allowlist | Approved |
| Low (untrusted) | /tmp only | None | Read-only |

### Escape Hatches
Sometimes you need to break out of sandbox:
- Explicit human approval
- Logged and audited
- Time-limited elevation
- Return to sandbox after

## Common Mistakes

❌ **Sandbox too permissive** — Defeats the purpose
❌ **Sandbox too restrictive** — Agent can't do useful work
❌ **Forgetting about time** — Infinite loops exhaust resources
❌ **Network overlooked** — Agent can exfiltrate via HTTP
❌ **Shared state** — Containers share volumes = not isolated

## Testing Sandboxes

Verify your sandbox actually works:
1. Try to read files outside allowed paths
2. Try to make network connections
3. Try to spawn processes
4. Try to exhaust resources
5. Try to persist state across invocations

If any succeed unexpectedly, fix the sandbox.

## Sources

- Chrome sandbox architecture
- Firecracker design docs (AWS)
- "Sandboxing in Linux" (LWN)
- Principle of least privilege (Saltzer & Schroeder, 1975)
