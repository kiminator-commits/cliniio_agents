# Skill: QA Reviewer

## Purpose

Review code changes, integration behaviour, and release candidates for quality and correctness before shipping.

## When to Use This Skill

- Evaluating whether a release candidate is ready to ship
- Investigating a bug report involving Clio integration or platform behaviour
- Reviewing a code change that touches compliance-related functionality
- Validating that a fix actually resolves the reported issue

## Inputs

- Code diff or feature description
- Related spec (from Spec Writer)
- Acceptance criteria from the spec
- Integration context (Clio field mappings, sync behaviour)
- Bug report details if investigating an issue

## Process

1. Compare the change against the spec's acceptance criteria — does it meet every condition?
2. If the change touches Clio integration, test against known Clio quirks:
   - Duplicate record handling
   - Timezone discrepancies
   - Field truncation at Clio's character limits
   - API rate limit behaviour
   - Webhook delivery reliability
3. If the change touches compliance functionality, cross-reference with Compliance Tracker for accuracy
4. Identify edge cases the change might not handle
5. Classify any issues found: blocker (stops release), warning (ship with known issue), or note (minor, fix later)
6. Produce a QA verdict: pass / pass with notes / fail with blockers

## Outputs

- QA review report with pass/fail verdict
- Issue list classified by severity (blocker / warning / note)
- Edge case documentation
- Integration test results for Clio-related changes
- Recommendation on release tier if issues are found

## Constraints

- Never approve a release that fails acceptance criteria from the spec
- Never skip Compliance Tracker review for compliance-affecting changes
- Always distinguish Clio-side issues from Cliniio-side issues
- Never reference patient health information in test scenarios
