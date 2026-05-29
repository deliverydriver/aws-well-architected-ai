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

## Services and Patterns for Demonstrating Depth

To show real fluency with the Well-Architected Framework on difficult, emerging workloads, this project will include rigorous, versioned reviews that go far beyond generic pillar checklists. The reviews will demonstrate deep, hands-on experience with:

**Well-Architected Framework Applied at Depth**
- Multiple full, evolving reviews of the architectures in aws-agent-platform and aws-landing-zone-for-ai (and sovereign patterns), updated across versions as real operational data comes in.
- Explicit "Agentic Systems Lens" guidance that extends the standard Framework for non-determinism, long-running state, human oversight as a reliability control, trajectory capture for audit/compliance, and cost volatility from inference.
- Quantitative elements in reviews: p99 agent turn latency, cost per successful task, mean time between human interventions, inference spend distribution, recovery time for stateful agents, etc.
- Honest trade-off analysis between pillars (e.g., Reliability vs Cost when using provisioned throughput vs on-demand; Security vs Performance when routing everything through approval proxies).

**Specific AWS Services & Features Used in Reviews**
- Heavy, opinionated use of X-Ray + OpenTelemetry for capturing full agent trajectories (model calls, tool invocations, state transitions, human decisions) — not just basic request tracing.
- AWS Cost and Usage Report (CUR) + Athena + custom attribution logic as core inputs to cost pillar reviews, including real (anonymized) spend analysis for different agent patterns.
- CloudWatch + Evidently or custom evaluation pipelines for operational excellence and reliability reviews of non-deterministic systems.
- AWS Config, Security Hub, GuardDuty, and Access Analyzer findings as primary data for security pillar reviews.
- Step Functions, EventBridge, and ECS/EKS service mesh / VPC Lattice patterns evaluated for reliability and operational excellence.
- Bedrock Guardrails, Model Invocation Logging, and SageMaker Model Monitor / Clarify as concrete controls in security, reliability, and cost reviews.
- Cross-account and cross-OU patterns (from the landing zone) analyzed for their impact on every pillar.

**Documentation That Proves Real Experience**
- Full pillar-by-pillar reviews with specific findings, risk ratings, and prioritized remediations tied to actual AWS features.
- Before/after architecture comparisons with measured impact.
- "What we got wrong the first time" sections with real lessons.
- Custom Well-Architected tooling or lenses developed for agentic workloads.

This becomes one of the strongest signals of deep architectural thinking and operational maturity.