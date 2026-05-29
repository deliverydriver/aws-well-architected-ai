# Well-Architected Review — AI Landing Zone (May 2026)

**Workload**: Multi-Account Landing Zone optimized for AI & Agentic Systems  
**Review Date**: 2026-05-29  
**Status**: Initial baseline review

## Workload Context

This is not a generic enterprise landing zone. It must support:
- High-velocity research/experimentation agents
- Production customer-facing agents with strict security and cost controls
- Significant cross-account tool calling
- Highly variable (and potentially expensive) inference workloads

## Pillar Summary

| Pillar                  | Rating     | Primary Risk Areas |
|-------------------------|------------|--------------------|
| Security                | Medium     | Tool execution blast radius, cross-account access |
| Reliability             | Medium     | Long-running agent state recovery |
| Operational Excellence  | Medium     | Drift detection at scale, exception processes |
| Cost Optimization       | High Risk  | Inference spend attribution and control |
| Performance Efficiency  | Medium     | Right-sizing for agent environments |
| Sustainability          | Low        | Not deeply reviewed |

## Key Findings

### Security — Medium

**Strengths**
- Good SCP strategy defined (see ADR 0001)
- Strong push toward PrivateLink + capability-based access

**High/Medium Findings**
- **HIGH**: Cross-account tool calling needs a mandatory approval proxy layer (currently designed but not yet implemented in all paths).
- **MEDIUM**: KMS key strategy for agent memory needs to be more prescriptive per OU.
- Need better workload identity story for agents that span multiple accounts.

### Cost Optimization — High Risk

This is the weakest area currently.

**Findings**
- **HIGH**: No production-grade mechanism yet for attributing inference spend to individual agents or experiments.
- **HIGH**: Budgets and anomaly detection exist at account level but not at the "agent session" granularity required.
- Need explicit strategy for when to use provisioned throughput vs on-demand in research vs production OUs.

### Reliability

**Findings**
- Long-running agent state (especially in Research OU) has limited multi-AZ / multi-region thinking today.
- Human approval workflows create a new single point of failure that needs reliability treatment.

### Operational Excellence

**Strengths**
- Strong ADR culture already visible.
- Good recognition that exception processes for SCPs are a first-class operational concern.

**Findings**
- Need automated drift detection and remediation for baseline configurations across dozens of accounts.
- Runbooks for "compromised agent" or "runaway cost agent" scenarios are still immature.

## Recommended Priorities (Next 90 Days)

1. Finish and deploy the approval proxy pattern for cross-account tool use (Security - HIGH)
2. Build session-level cost attribution + basic automated throttling (Cost - HIGH)
3. Define and implement workload identity for agents (Security)
4. Create first version of "runaway agent" operational runbooks

## Overall Assessment

The landing zone has a strong conceptual foundation and the right biases (AI-native, research vs production separation, cost sensitivity). The main gaps are execution depth on cost control and the security boundary around tool execution.

This is a solid starting point for a specialized landing zone. The next 3-6 months of real usage will be the real test.

---
*This review will be updated after the first wave of production agent workloads are running.*