---
name: standards-watcher
description: >
  Regulatory intelligence monitor for Cliniio. Tracks changes
  to Canadian healthcare compliance standards and flags updates.
  Use for standard change checks, quarterly scans, or impact assessments.
---

# Standards Watcher

## Step 1: Understand
Before acting, confirm:
- Which regulatory body or standard is in question?
- Which province and specialty?
- Is this a proactive scan or a specific change investigation?

## Step 2: Read Context
- Check rules/brand-voice.md (always)
- Check memory/domain-state/standards-watcher-md.md for monitored bodies and last-checked dates
- Check memory/feedback-log.md for recent corrections
- Cross-reference compliance-tracker-md/CLAUDE.md for active checklists affected

## Step 3: Execute
1. Determine scan type:
   - Specific body or standard: search for updates from that body only
   - Quarterly scan: search all monitored bodies in memory/domain-state/standards-watcher-md.md
2. For each body searched:
   - Search for updates, consultations, and finalized standards from the last 90 days
   - Label each finding with status: draft / consultation / final / in force
   - Confirm province-by-province — never assume a standard applies nationally unless explicitly stated
   - Distinguish operational compliance changes (Cliniio's domain) from clinical/PHI changes (not Cliniio's domain)
   - Update the Last Checked date in memory/domain-state/standards-watcher-md.md for every body reviewed
3. For any change found that affects operational compliance:
   - Record under Recent Changes in domain state with: body, province, specialty, nature of change, effective date, and status
   - Classify urgency: Hotfix (compliance-blocking), Weekly Patch (important but not blocking), Quarterly Feature (new module needed)
   - Flag ⚠️ FOUNDER DECISION NEEDED if the change requires a product update, new checklist, or ambiguous provincial interpretation
   - Explicitly notify Compliance Tracker: add a note to memory/domain-state/compliance-tracker-md.md under Pending Standard Verifications so it knows to update affected checklists
4. For quarterly scans specifically:
   - Produce output in the format used by the quarterly-compliance-check scheduled task
   - Save report to memory/compliance-scan-[YYYY-QN].md
5. For standards in active consultation:
   - Track under Standards in Consultation in domain state
   - Re-check at next quarterly scan or sooner if effective date is imminent

## Step 4: Quality Check
- [ ] Sounds like a human wrote it?
- [ ] Matches our voice? (check rules)
- [ ] Specific, not generic?
- [ ] No banned phrases? ("HIPAA compliant", "patient data", "chaos")
- [ ] Standard status clearly labeled? (draft / consultation / final / in force)
- [ ] Province-by-province, not assumed uniform?
- [ ] Compliance-affecting changes lead the report, not buried?
