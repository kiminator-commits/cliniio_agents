# Cliniio Agent Manifest

## Active Agents

| Agent | Directory | Domain | Status |
|---|---|---|---|
| Chief of Staff | `chief-of-staff/` | Daily ops, triage, coordination | Active |
| Release Manager | `release-manager/` | Shipping, versioning, deploys | Active |
| Compliance Tracker | `compliance-tracker/` | Regulatory checklists, gap analysis | Active |
| Funding Scout | `funding-scout/` | Grants, SRED, accelerators | Active |
| Prospect Filter | `prospect-filter/` | Lead qualification, outreach prep | Active |
| Clio QA | `clio-qa/` | Clio integration, sync, field mapping | Active |
| Spec Writer | `spec-writer/` | Feature specs, user stories | Active |
| Standards Watcher | `standards-watcher/` | Regulatory updates, standard changes | Active |
| Audit Scribe | `audit-scribe/` | Audit docs, binder formatting | Active |
| Advisor | `advisor/` | Strategy, pricing, positioning | Active |

## Shared Resources

- **Rules:** `.claude/rules/brand-voice.md`
- **Skills:** `.claude/skills/`
- **Domain State:** `memory/domain-state/`
- **Lessons Learned:** `memory/lessons.md`
- **Feedback Log:** `memory/feedback-log.md`
- **Preferences:** `config/preferences.md`

## Agent Lifecycle

1. Agent receives a routed request (from Chief of Staff or direct)
2. Agent reads its own `CLAUDE.md` for role context
3. Agent checks `memory/domain-state/[agent].md` for current state
4. Agent produces output
5. Agent updates its domain state file
6. If the output needs founder review, agent flags `⚠️ FOUNDER DECISION NEEDED`

## Last Updated

2026-04-13
