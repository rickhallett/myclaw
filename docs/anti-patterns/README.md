# Anti-Patterns

What doesn't work in agentic systems—and why.

## Purpose

Learning from failure is faster than rediscovering it. This section documents approaches that seem reasonable but cause problems in practice.

## Index

*Add entries as anti-patterns are documented.*

### Common Anti-Patterns

- **YOLO Mode** — Agent with unrestricted capabilities "because it's faster"
- **Context Stuffing** — Cramming everything into context instead of using retrieval
- **Trust Cascade** — Agent A trusts Agent B trusts external data = transitive trust failure
- **Retry Storm** — Exponential retries without backoff or circuit breakers
- **Capability Creep** — Starting minimal then adding tools until you have ambient authority again

### Coming Soon

- God Agent (one agent does everything)
- Implicit State (relying on conversation context for critical state)
- Security Theater (sandboxing that doesn't actually sandbox)

## Contributing

Found an anti-pattern the hard way? Document it:

1. Name it (memorable helps)
2. Describe what it looks like
3. Explain why it fails
4. Suggest alternatives

See [CONTRIBUTING.md](../../CONTRIBUTING.md) for style guide.
