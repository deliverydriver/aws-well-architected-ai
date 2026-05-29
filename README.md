# Well-Architected Reference Architectures for AI Systems on AWS

**A living collection of real, reviewed, and continuously improved reference architectures for modern AI workloads on AWS — with full Well-Architected Framework reviews (including the new AI/ML Lens where applicable).**

This project exists to close the gap between "I know the six pillars" and "I can actually design, review, and improve complex AI systems using the framework."

## Why This Strengthens Applications

The Well-Architected Framework is one of the most practical and frequently referenced parts of the Solutions Architect Professional exam and real consulting work.

Most candidates can recite the pillars.

Top candidates can:
- Conduct a real review
- Identify specific high-risk issues
- Propose concrete, prioritized remediations
- Do this for emerging workload types (agentic systems, RAG pipelines, voice agents, autonomous workflows)

This repo gives you a portfolio of exactly that.

### Exam + Interview Value

| Area | How This Helps |
|------|----------------|
| Exam Domain: Design for existing solutions | You will be given scenarios and asked to improve them. This repo is practice at scale. |
| Well-Architected questions in interviews | You can say "I maintain a public set of reviews for AI workloads and have iterated on them multiple times." |
| Consulting credibility | Clients love seeing that you don't just deploy — you review and improve against a standard. |

## What This Repository Contains

For each reference architecture:

1. **Clear problem statement** (what real-world situation this solves)
2. **Architecture diagram** (Mermaid + high-quality exports)
3. **Detailed Well-Architected review** (all pillars + AI/ML Lens)
4. **High/Medium/Low risk findings** with specific AWS service recommendations
5. **Remediation backlog** (prioritized, with rough effort)
6. **Evolution notes** — what we changed in later iterations and why
7. **Cost model** and trade-off analysis

## Current & Planned Reference Architectures

### Tier 1 (High Priority)

- **Production Voice Agent Platform** (ties directly to aws-agent-platform)
- **Secure RAG / Knowledge Platform** at scale (Kendra + Bedrock + OpenSearch Serverless + proper access control)
- **Long-running Autonomous Agent Orchestration Platform** (the "Omen-class" system)
- **Cost-Optimized Batch Inference & Fine-Tuning Pipeline**

### Tier 2

- Multi-tenant AI SaaS platform (with strong isolation)
- Real-time multimodal agent system (vision + voice)
- Sovereign / air-gapped AI inference environment
- Agent evaluation and continuous improvement platform

## Principles

- We review **realistic** architectures, not toy examples.
- Every review is versioned. We show how the architecture improved over time.
- We are honest about trade-offs (especially cost vs security vs latency for AI workloads).
- Findings are specific ("Use this specific feature of Guardrails + this SCP") rather than generic.

## Well-Architected Lens Usage

- Standard six pillars
- AWS Well-Architected Framework – AI/ML Lens (when officially available / as it evolves)
- Custom "Agentic Systems" considerations we develop over time (state management, non-determinism, human oversight as a pillar concern, tool-use security, etc.)

## Relationship to the Rest of the Portfolio

This project is the **review and improvement layer** on top of the concrete implementations in:
- `aws-agent-platform`
- `aws-landing-zone-for-ai`
- `aws-sovereign-infrastructure`

## Current Status

Early scaffold. The first full reviews will be published as the other projects mature enough to be worth reviewing.

## How This Will Be Used in Exam Prep

I will regularly conduct formal Well-Architected reviews of my own work and publish the results here. This creates:
- Deep muscle memory for the exam
- Artifacts I can actually show in interviews
- A public body of work that demonstrates operational maturity

---

This is one of the highest-leverage things you can do while preparing for the Solutions Architect Professional exam if you want to stand out.

Built by Benjamin Pittman while studying for the AWS Certified Solutions Architect – Professional exam.
