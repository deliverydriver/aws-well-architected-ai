# Reference Architectures and Operational Reviews for AI Systems on AWS

A collection of reference implementations for AI and agentic workloads on AWS, accompanied by detailed, ongoing operational and architectural reviews.

## Purpose

Most published AWS architecture examples are either simple getting-started patterns or high-level reference diagrams. This repository aims at something narrower and more useful: concrete designs for real classes of AI system (long-running agents, voice interfaces, secure tool use, RAG at scale, etc.), reviewed against the actual constraints those systems face in production.

The reviews are not one-time artifacts. They are updated as the designs evolve, as new services appear, and as operational experience accumulates.

## Scope of Reviews

Reviews cover the full set of concerns that matter for these workloads:

- Security boundaries around agent capabilities and tool execution
- Reliability and state management for processes that can run for hours or days
- Cost modeling and controls when the primary variable cost is non-deterministic inference
- Observability and debugging of systems whose behavior is not fully predictable from the code
- Operational load on the teams running the systems
- Data sovereignty and residency constraints

Where relevant, the reviews explicitly call out where standard Well-Architected guidance needs extension or modification for agentic and stateful AI workloads.

## Current Coverage

The repository is being populated alongside the other projects in this set. Initial reviews focus on the architectures defined in aws-agent-platform and the governance model in aws-landing-zone-for-ai.

Each review includes:
- The driving requirements and constraints
- The chosen architecture and major alternatives considered
- Specific findings (high/medium/low) with concrete remediation options
- Trade-off rationale
- Open questions and areas under active revision

## Approach

- Specificity over generality. "Use PrivateLink for this particular tool server" is more valuable than "consider using PrivateLink."
- Production experience over theoretical purity. Designs are judged by how they behave under real load, real cost pressure, and real security incidents.
- Explicit treatment of AI-specific problems (trajectory capture, approval latency vs. user experience, attribution of inference spend to individual agent sessions, etc.).
- No sacred cows. If a pattern that looks good on paper creates unacceptable operational load or cost volatility in practice, that is documented.

## Relationship to the Rest of the Work

These reviews are the analytical layer on top of the concrete implementations in the other repositories. The goal is a tight feedback loop: build, operate, review, adjust, document.

---

The value is in the precision of the analysis and the willingness to revise earlier decisions when reality disagrees with the model. This is reference material for people who are already building these classes of system.