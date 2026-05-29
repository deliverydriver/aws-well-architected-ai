# Well-Architected Review — Agent Platform (May 2026)

**Workload**: Production Voice-Controlled and Autonomous Agent Platform  
**Review Date**: 2026-05-29  
**Reviewers**: [Your name]  
**Status**: Initial review — will be updated after 3 months of production data

## Summary

This is a stateful, tool-using, voice-enabled agent platform. It has very different characteristics from traditional request/response applications.

**Overall Risk Profile**: Medium-High (mainly due to non-determinism + tool use + cost volatility)

## Pillar Assessments

### Security
**Rating**: Medium

**Strengths**
- Strong defense-in-depth on tool execution (see ADR 0001)
- Workload identity patterns in place
- PrivateLink usage for model and tool calls

**High/Medium Findings**
- **HIGH**: Agent memory stores need envelope encryption + Macie scanning (currently planned but not fully implemented)
- **MEDIUM**: Need better runtime protection against prompt injection leading to dangerous tool calls
- Need to formalize the "capability classification" process as code

### Reliability
**Rating**: Medium

**Strengths**
- Step Functions used for long-running sessions with proper error handling
- Good separation of execution environments

**Findings**
- **MEDIUM**: Recovery of long-running agent state after regional impairment needs more work
- No chaos engineering yet for agent failure modes

### Performance Efficiency
**Rating**: Medium-Low

**Findings**
- Heavy use of on-demand inference in many places — should evaluate provisioned throughput + caching layers
- Need better right-sizing for agent execution environments

### Cost Optimization
**Rating**: High Risk Area

**Strengths**
- Good attribution work starting

**Findings**
- **HIGH**: Inference spend is not yet fully attributed to individual agent sessions/customers in production
- No automated kill switches or budget-based throttling in production yet
- Need to model the cost of human approval latency vs cheaper models

### Operational Excellence
**Rating**: Medium

**Strengths**
- Good ADR culture
- Strong desire for observability of agent trajectories

**Findings**
- Need better automated canary + evaluation pipelines before promoting new agent versions
- Runbooks for "runaway agent" scenarios are still manual

### Sustainability
Not deeply reviewed yet.

## Recommended Next Actions (Prioritized)

1. Finish envelope encryption + Macie on agent memory (Security - HIGH)
2. Implement session-level cost attribution + basic throttling (Cost - HIGH)
3. Build proper evaluation + canary deployment pipeline for agents (Operational Excellence)
4. Add regional DR story for long-running agent state (Reliability)

---

This review will be re-run after we have real production telemetry.
