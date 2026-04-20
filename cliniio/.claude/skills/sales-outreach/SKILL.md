# Skill: Sales Outreach

## Purpose

Qualify prospects against Cliniio's ideal customer profile and prepare outreach materials for approved leads.

## When to Use This Skill

- Evaluating whether a clinic is a good fit for Cliniio
- Filtering a list of potential prospects
- Preparing outreach briefs for qualified leads
- Assessing a new region or territory for prospect density

## Inputs

- Clinic name, location, specialty, and any known details
- Province and regulatory body context
- Existing disqualification log (from `memory/domain-state/prospect-filter.md`)

## Process

1. Run the prospect through the five-point qualification filter:
   - **Specialty match** — dental, medical, or allied health that Cliniio supports
   - **Size fit** — independent, 1–5 operatories/exam rooms, max 2–3 locations
   - **Vendor entanglement** — not embedded in Telus Health ecosystem → instant disqualify if yes
   - **Province coverage** — in any Canadian province or territory (ON, QC, BC, AB, MB, SK, NS, NB, NL, PEI, NT, YT, NU) where Cliniio has mapped standards
   - **Tech readiness** — has a website, uses some cloud tools, not entirely paper-based
2. Assign a verdict: pass / fail / maybe
3. For "maybe" prospects, flag for founder review with the specific concern
4. For qualified prospects, draft an outreach-ready brief

## Outputs

- Prospect scorecards with per-criterion verdicts
- Filtered and prioritized prospect lists (high / medium / low fit)
- Disqualification log entries with reasons
- Outreach-ready briefs with clinic context and suggested angle

## Constraints

- Never draft outreach for unqualified prospects
- Never skip the Telus Health vendor check
- Never qualify a clinic in an unsupported province
- All outreach requires founder approval before sending
- Follow brand voice rules — no salesy language
