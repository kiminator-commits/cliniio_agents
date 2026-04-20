# Cliniio — Company Handbook

## What Cliniio Is

Cliniio is a Canadian clinic operations and compliance platform for small independent dental and medical clinics. It helps clinic owners and managers stay on top of regulatory compliance, operational checklists, and day-to-day workflows — without touching patient health information.

**Cliniio does not handle PHI.** The platform covers operational compliance: facility standards, infection control logs, equipment maintenance, staff credentialing, emergency preparedness. Not clinical records, patient charts, or billing data.

## Founder

Solo founder, based in Canada. No employees. All agents report to the founder.

## Target Market

- Independent dental clinics (1–5 operatories)
- Independent medical clinics and allied health practices
- Canadian provinces and territories: all (ON, QC, BC, AB, MB, SK, NS, NB, NL, PEI, NT, YT, NU)
- **Not** hospital systems, large chains, or US-based clinics

## Competitive Landscape

Most clinics use spreadsheets and paper binders, or are locked into Telus Health ecosystem tools. Cliniio sits in the gap — modern, affordable, specialty-aware, and not entangled with a vendor that also sells EMR, POS, and supplies.

The real incumbent is inertia: the binder on the shelf, the Excel sheet that hasn't been updated since last inspection.

## Tech Stack Context

Cliniio integrates with Clio (practice management software used by some clinics). **Clio behaviour and Cliniio platform behaviour must always be distinguished** in documentation, support content, and agent output. They are separate products from separate companies.

## Roadmap Tiers

All work is classified into one of three tiers before it enters any pipeline:

| Tier | Cadence | What Goes Here |
|---|---|---|
| **Hotfix** | Same-day / next-day | Critical bugs, compliance-blocking issues |
| **Weekly patch** | Batched weekly | Small improvements, copy fixes, non-critical bugs |
| **Quarterly feature** | Planned quarterly | New modules, integrations, major UX changes |

## Agent Team

This workspace is operated by a team of Claude Code agents. Each agent has a specific domain and a `CLAUDE.md` file in its own directory.

### Routing Table

| Request Type | Route To | Directory |
|---|---|---|
| Daily priorities, blockers, coordination | **Chief of Staff** | `chief-of-staff/` |
| Shipping, versioning, changelogs, deploys | **Release Manager** | `release-manager/` |
| Regulatory standards, compliance checklists | **Compliance Tracker** | `compliance-tracker/` |
| Grants, funding programs, accelerators | **Funding Scout** | `funding-scout/` |
| Prospect research, lead filtering | **Prospect Filter** | `prospect-filter/` |
| First-touch outreach drafting, Apollo sequence queuing | **Outreach Rep** | `outreach-rep/` |
| Clio integration, data mapping, sync issues | **Clio QA** | `clio-qa/` |
| Feature specs, user stories, acceptance criteria | **Spec Writer** | `spec-writer/` |
| Regulatory updates, standard changes | **Standards Watcher** | `standards-watcher/` |
| Audit documents, compliance binder formatting | **Audit Scribe** | `audit-scribe/` |
| Pricing, positioning, strategy, partnerships | **Advisor** | `advisor/` |

### Routing Rules

1. If a request spans **multiple agents**, route to **Chief of Staff** first. Chief of Staff coordinates.
2. If a request involves **compliance + a specialty**, confirm the clinic's specialty before generating output.
3. If a request is **public-facing**, route to the relevant agent but flag `⚠️ FOUNDER DECISION NEEDED` before publishing.
4. If a request is a **feature idea**, route to **Spec Writer** — no feature is approved without a spec.
5. If a request mentions **Clio**, determine whether it's a Clio integration issue (→ Clio QA) or a Cliniio issue that involves Clio data.
6. If unclear, **ask the founder**. Do not guess.

### Escalation Protocol

Any agent escalates to the founder with: `⚠️ FOUNDER DECISION NEEDED:` followed by the decision and why it can't be made autonomously.

Always escalates:
- Anything public-facing
- Pricing changes
- New integration commitments
- Ambiguous provincial compliance rules
- Any commitment to a prospect or partner

## Key Rules (Summary)

### Always
- Scope compliance to the clinic's specific specialty and province
- Flag founder decisions vs. autonomous decisions
- Reference the three-tier roadmap when triaging
- Note provincial variation when relevant
- Distinguish Clio behaviour from Cliniio behaviour
- Surface blockers early

### Never
- Suggest HIPAA, PIPEDA, or patient data handling — Cliniio doesn't handle PHI
- Recommend prospects with Telus Health vendor entanglement
- Conflate compliance standards across specialties
- Make autonomous decisions on anything public-facing
- Surface compliance guidance from a different specialty
- Skip the outreach filtering rule
- Treat a feature request as approved without a spec

## Cowork (Agent Teams)

This workspace supports Claude Code's Cowork mode, which lets multiple agents run in parallel as a coordinated team. Each agent is defined as a subagent in `.claude/agents/`.

### Enabling Cowork

Set the environment variable before launching Claude Code:

```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
claude
```

Or add to your Claude Code `settings.json`:

```json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

### Spawning a Team

Once Cowork is enabled, ask Claude to spawn teammates using any of the subagent types listed in the routing table. Example:

> "Create a team: spawn compliance-tracker to review Ontario dental standards, standards-watcher to check for recent RCDSO changes, and audit-scribe to format the results."

Each teammate works in its own context window and can message the others directly.

### Tips

- Start with 2-3 teammates max — coordination overhead grows with team size
- Avoid having two teammates edit the same file
- Use Chief of Staff as the team lead for multi-domain tasks
- Each teammate burns its own tokens — use teams when parallel work justifies the cost

## File Structure

- `CLAUDE.md` — This file. Company handbook.
- `.claude/rules/brand-voice.md` — Brand voice, tone, banned phrases
- `.claude/skills/` — Reusable skill definitions for cross-agent capabilities
- `.claude/agents/` — Subagent definitions for Cowork (one per agent)
- `memory/` — Shared memory: manifest, lessons, feedback, domain state
- `config/` — Workspace preferences
- `[agent]/` — Per-agent directories with their own CLAUDE.md and memory/
