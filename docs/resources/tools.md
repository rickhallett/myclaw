# Tools & Frameworks

Software for building agentic systems.

## Agent Frameworks

### LangChain / LangGraph
- **URL:** https://langchain.com
- **What:** Popular framework for LLM applications and agents
- **Notes:** Large ecosystem, can be over-engineered for simple cases

### AutoGen
- **URL:** https://microsoft.github.io/autogen/
- **What:** Microsoft's multi-agent conversation framework
- **Notes:** Good for multi-agent patterns, heavy dependencies

### CrewAI
- **URL:** https://www.crewai.com/
- **What:** Role-based multi-agent framework
- **Notes:** Simpler than AutoGen, opinionated about agent roles

### Semantic Kernel
- **URL:** https://github.com/microsoft/semantic-kernel
- **What:** Microsoft's SDK for LLM integration
- **Notes:** Good for .NET/enterprise environments

## Security

### wasp
- **URL:** https://github.com/rickhallett/wasp
- **What:** Security whitelist layer for agentic systems
- **Notes:** Capability-based tool restrictions. From the sandcastle architecture.

### Guardrails AI
- **URL:** https://guardrailsai.com/
- **What:** Input/output validation for LLMs
- **Notes:** Useful for constraining agent behavior

### Rebuff
- **URL:** https://github.com/protectai/rebuff
- **What:** Prompt injection detection
- **Notes:** Defense layer, not complete solution

## Sandboxing

### E2B
- **URL:** https://e2b.dev/
- **What:** Sandboxed cloud environments for AI agents
- **Notes:** Easy to use, handles isolation for you

### Firecracker
- **URL:** https://firecracker-microvm.github.io/
- **What:** Lightweight VMs for serverless/containers
- **Notes:** What Lambda uses. Fast, secure, more complex to set up.

### gVisor
- **URL:** https://gvisor.dev/
- **What:** Application kernel for containers
- **Notes:** Stronger isolation than standard containers

## Evaluation

### AgentBench
- **URL:** https://github.com/THUDM/AgentBench
- **What:** Benchmark for LLM agents
- **Notes:** Test your agent against standardized tasks

### HELM
- **URL:** https://crfm.stanford.edu/helm/
- **What:** Holistic LLM evaluation
- **Notes:** Broader than agents, useful for model selection

## Observability

### LangSmith
- **URL:** https://smith.langchain.com/
- **What:** Tracing/debugging for LLM apps
- **Notes:** Works with LangChain, useful for debugging agent flows

### Weights & Biases
- **URL:** https://wandb.ai/
- **What:** ML experiment tracking
- **Notes:** Not agent-specific but useful for tracking agent behavior

---

*Add tools with URL, one-line description, and honest notes on tradeoffs.*
