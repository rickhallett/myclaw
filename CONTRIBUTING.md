# Contributing to myclaw

## The Goal

Capture distilled, actionable knowledge about building agentic systems. Not a link dump — a curated field manual.

## What Belongs Here

✅ **Yes:**
- Battle-tested patterns with clear explanations
- Security considerations with concrete mitigations
- Failure modes you've seen (or caused) with lessons learned
- Curated links to exceptional resources

❌ **No:**
- Raw article dumps without synthesis
- Speculation without evidence
- Vendor-specific tutorials (keep it general)
- Obvious/trivial advice

## Document Style

### Structure

```markdown
# Title

One-sentence summary of the insight.

## The Pattern / The Problem / The Approach

Clear explanation. What, why, when.

## Example

Concrete illustration. Code optional but helpful.

## When to Use / When to Avoid

Applicability guidance.

## Sources

- [Author, "Title"](url) — Brief note on relevance
```

### Writing Guidelines

1. **Lead with the insight** — Don't bury the lede
2. **Be specific** — "Use capability-based security" beats "be careful"
3. **Show tradeoffs** — Every pattern has costs
4. **Cite sources** — Original work deserves credit
5. **Keep it scannable** — Headers, bullets, short paragraphs

## File Naming

- Lowercase, hyphenated: `prompt-injection.md`
- Descriptive but brief
- Match existing conventions in the directory

## Adding Resources

For `docs/resources/`:
- Include title, author, URL
- Add one line explaining why it's worth reading
- Categorize appropriately (blog, paper, tool)

## Pull Requests

1. One topic per PR
2. Explain what knowledge you're adding and why
3. Self-review for clarity before requesting review

## Questions?

Open an issue. We're here to help.
