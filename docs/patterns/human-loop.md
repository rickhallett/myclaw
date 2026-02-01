# Human-in-the-Loop Design

When and how to involve humans in agentic workflows.

## The Principle

Agents should operate autonomously within safe bounds, but escalate to humans for:
- Irreversible actions
- Ambiguous decisions
- High-stakes choices
- Novel situations outside training

## Escalation Triggers

### Always Ask
- Deleting data (especially without backup)
- Sending external communications (email, posts, payments)
- Actions with legal/financial implications
- Anything the user explicitly marked as sensitive

### Ask First Time, Remember Preference
- Recurring operational decisions
- Style/format preferences
- Tool selection when multiple options exist

### Act Then Report
- Low-risk, reversible operations
- Routine tasks within established patterns
- Information gathering (search, read)

## Design Patterns

### Confirmation Gates

```
Agent: I'm about to delete 47 old log files (2.3GB). Proceed? [y/N]
Human: y
Agent: Done. Deleted 47 files.
```

Keep confirmations:
- Specific (what exactly will happen)
- Quantified (how much, how many)
- Defaulting to safe option (N for destructive)

### Approval Queues

For async workflows:
1. Agent queues action with explanation
2. Human reviews batch when available
3. Approved actions execute; rejected get feedback

Good for: scheduled tasks, bulk operations, non-urgent decisions

### Confidence Thresholds

```python
if confidence > 0.95:
    execute()
elif confidence > 0.7:
    execute_and_notify()
else:
    request_human_input()
```

Calibrate thresholds based on:
- Action reversibility
- Blast radius of errors
- User's risk tolerance

### Audit Trails

Even autonomous actions should be logged:
- What was decided
- Why (reasoning/confidence)
- What happened
- Easy to review later

## Anti-patterns

❌ **Asking too often** — Alert fatigue leads to rubber-stamping
❌ **Vague confirmations** — "Proceed with operation?" tells user nothing
❌ **No undo path** — If human approves wrongly, recovery should be possible
❌ **Blocking on non-critical** — Don't halt workflows for trivial decisions

## The Sweet Spot

```
┌─────────────────────────────────────────────────┐
│                   Agent Autonomy                │
│                                                 │
│   Low Risk ◄──────────────────────► High Risk   │
│   Reversible                       Irreversible │
│   Routine                          Novel        │
│                                                 │
│   ◄─── More Autonomous    More Human Input ───► │
└─────────────────────────────────────────────────┘
```

## Sources

- "Human-in-the-Loop Machine Learning" (Monarch, 2021)
- Automation levels in self-driving (SAE J3016)
- "Ironies of Automation" (Bainbridge, 1983)
