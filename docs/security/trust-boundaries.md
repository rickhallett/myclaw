# Trust Boundaries

Where to draw lines between trusted and untrusted components in agentic systems.

## The Concept

A trust boundary is a line in your system where data or control flow crosses between components with different trust levels. Every crossing is a potential vulnerability.

## Trust Levels in Agentic Systems

### Fully Trusted
- System prompts
- Core orchestration code
- Hardcoded tool implementations

### User-Trusted
- User's direct instructions
- User's files (mostly—could be compromised)
- User's authenticated sessions

### Untrusted
- Web content fetched by agent
- Third-party API responses
- Files from external sources
- Other agents' outputs
- Anything that could contain prompt injection

## Identifying Boundaries

```
┌─────────────────────────────────────────────────────┐
│                    TRUSTED ZONE                      │
│  ┌─────────────┐    ┌─────────────┐                │
│  │   System    │    │   User      │                │
│  │   Prompt    │    │   Input     │                │
│  └─────────────┘    └─────────────┘                │
│         │                  │                        │
│         ▼                  ▼                        │
│  ┌─────────────────────────────────┐               │
│  │          COORDINATOR            │               │
│  └─────────────────────────────────┘               │
│                    │                                │
└────────────────────┼────────────────────────────────┘
                     │ ◄─── TRUST BOUNDARY
┌────────────────────┼────────────────────────────────┐
│                    ▼          UNTRUSTED ZONE        │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐         │
│  │ Web      │  │ External │  │ Worker   │         │
│  │ Content  │  │ APIs     │  │ Outputs  │         │
│  └──────────┘  └──────────┘  └──────────┘         │
└─────────────────────────────────────────────────────┘
```

## Rules for Boundary Crossings

### Entering Trusted Zone (Untrusted → Trusted)
1. **Validate** — Check data matches expected format
2. **Sanitize** — Remove or escape dangerous content
3. **Constrain** — Limit what untrusted data can influence
4. **Log** — Record what crossed and when

### Leaving Trusted Zone (Trusted → Untrusted)
1. **Minimize** — Send only what's necessary
2. **Redact** — Remove sensitive information
3. **Sign/Encrypt** — If data must remain tamper-proof

## Practical Applications

### Tool Invocation
```
User: "Search the web for X"
       │
       ▼
[TRUSTED] Coordinator decides to call search tool
       │
       ▼ ← BOUNDARY: sanitize query
[UNTRUSTED] Web search executes
       │
       ▼ ← BOUNDARY: validate/constrain results
[TRUSTED] Coordinator processes results
```

### Multi-Agent Systems
```
[TRUSTED] Coordinator Agent
       │
       ▼ ← BOUNDARY: task description only
[LOWER TRUST] Worker Agent
       │
       ▼ ← BOUNDARY: validate output, don't trust blindly
[TRUSTED] Coordinator aggregates
```

### File Processing
```
[TRUSTED] User requests: "Summarize this PDF"
       │
       ▼
[TRUSTED] Coordinator opens file
       │
       ▼ ← BOUNDARY: file content is untrusted!
[CONSTRAINED] Summarization with limited capabilities
       │
       ▼ ← BOUNDARY: output validation
[TRUSTED] Return summary to user
```

## Common Mistakes

❌ **Trusting agent outputs** — Just because your agent produced it doesn't mean it's safe
❌ **Trusting user files** — Could be malicious or compromised
❌ **Flat trust model** — Everything equally trusted = no defense
❌ **Boundary without enforcement** — Drawing lines means nothing without checks

## Design Principles

1. **Minimize trust** — Default to untrusted; upgrade explicitly
2. **Explicit boundaries** — Document where they are
3. **Defense in depth** — Multiple boundaries, not just one
4. **Fail secure** — On error, deny rather than allow

## Sources

- STRIDE threat modeling (Microsoft)
- "Threat Modeling" (Shostack, 2014)
- Zero trust architecture (NIST SP 800-207)
