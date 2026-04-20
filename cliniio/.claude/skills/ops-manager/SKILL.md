# Skill: Ops Manager

## Purpose

Handle day-to-day operational workflows: compliance tracking, audit prep, standards monitoring, and documentation formatting.

## When to Use This Skill

- Building or updating compliance checklists for a specific clinic type and province
- Preparing audit-ready documentation
- Monitoring regulatory standard changes
- Formatting inspection logs and compliance binders
- Tracking record retention schedules

## Inputs

- Clinic specialty (dental, medical, allied health)
- Province or territory (any Canadian province or territory: ON, QC, BC, AB, MB, SK, NS, NB, NL, PEI, NT, YT, NU)
- Specific regulatory body (RCDSO, CPSO, CDSBC, etc.)
- Audit type if applicable (routine, complaint-driven, random)
- Raw compliance data to format

## Process

1. Confirm specialty and province — never proceed without these
2. Check `memory/domain-state/standards-watcher.md` for recent standard changes
3. Pull the relevant standard requirements for the clinic's specialty and province
4. Cite source standard and section number for every compliance item
5. Distinguish operational compliance (Cliniio's domain) from clinical/PHI compliance (not Cliniio's domain)
6. Format output for the target audience:
   - For clinic managers: plain language, actionable items
   - For auditors: precise, dated, with signature fields
   - For internal use: structured, cross-referenced

## Outputs

- Province- and specialty-specific compliance checklists with source citations
- Gap analyses (covered / not covered / partial)
- Audit binder tables of contents
- Formatted inspection logs with date and initial fields
- Record retention schedules
- Provincial comparison tables
- Standard change alerts with Cliniio impact assessment

## Constraints

- Never generate HIPAA or PIPEDA guidance
- Never mix standards across specialties
- Never produce compliance guidance without specifying province and regulatory body
- Never claim Cliniio is "compliant with" a standard — Cliniio helps clinics track compliance
- Never fabricate compliance records or suggest backdating
- Always add a "last verified" date to formatted documents
