# Vizcraft Agent Architecture

*Created: January 21, 2026*
*Milestone: First sale completed 🚀*

---

## The Vision

Build a **semi-autonomous agent company** where agents execute and Ricardo reviews. Shift from human-driven to agent-driven operations.

---

## Current Agent State

| Agent | Role | Current | Potential |
|-------|------|---------|-----------|
| FRIDAY 🛠️ | DevOps/Releases | Release monitoring | Sentry→Code pipeline |
| ORACLE 🔍 | Research | Research | SEO/Trends analysis |
| COULSON 📋 | Coordination | Undefined | Issue tracking |
| ARCHIVIST 📚 | Memory | Knowledge base | Could support all agents |
| KODA 🐦 | Family chat | Conversational | Leave as-is |

---

## Proposed Architecture

```
         RICARDO (Review & Approve)
                 │
              JARVIS ⚡️ (Orchestrator)
                 │
    ┌────────────┼────────────┼────────────┐
    │            │            │            │
 GROWTH      DEVGUARD      CONTENT      ORACLE
 (Ads/SEO)   (Sentry→PR)   (Posts)      (Deep Research)
    │            │            │            │
 PostHog      Sentry      SEO/Social    Trends/Competitors
```

---

## Agent Responsibilities

### FRIDAY (DevGuard)
- Monitor Sentry for errors
- Create GitHub issues from errors
- Trigger Codex/Claude Code to fix
- Open PRs for review
- Release monitoring (existing)

### ORACLE (Research)
- Weekly SEO trend analysis
- Competitor research
- Content opportunities
- Market insights

### GROWTH (New)
- PostHog data analysis
- Ad platform monitoring
- Budget optimization recommendations
- Performance reports

### CONTENT (New)
- Draft SEO posts from Oracle's research
- Social media content
- Auto-schedule after review

---

## Automation Levels

| Task | Autonomy | Human Touch |
|------|----------|-------------|
| Sentry error → PR | High | PR review only |
| Ad budget adjust | High | Weekly report |
| SEO post creation | Medium | Pre-publish review |
| PostHog insights → Strategy | Low | Ricardo decides |

---

## Implementation Phases

### Phase 1 (This Week)
- [ ] FRIDAY + Sentry integration
- [ ] Oracle → Weekly SEO research reports

### Phase 2 (Next)
- [ ] GROWTH agent for PostHog + ads
- [ ] CONTENT agent for automated posts

---

## Tech Stack Notes

- MiniMax API configured for all agents
- Claude Code/Codex for coding tasks
- PostHog API for analytics
- Sentry API for error monitoring
- Clawdbot for orchestration

---

## Key Outcomes

1. **Reduce human time** in day-to-day operations
2. **Faster feedback loops** from errors to fixes
3. **Consistent marketing** with Oracle→Content pipeline
4. **Data-driven decisions** with GROWTH agent insights

---

*Next: Sketch Sentry→PR pipeline implementation*
