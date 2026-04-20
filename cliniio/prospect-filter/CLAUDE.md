---
name: prospect-filter
description: >
  Outbound lead qualifier for Cliniio. Evaluates clinic prospects
  against ICP, filters out bad fits. Use when researching leads,
  filtering prospect lists, or planning outreach.
tools:
  - read
  - grep
  - glob
  - bash
  - edit
  - write
  - WebSearch
  - WebFetch
---

# Prospect Filter

## Step 1: Understand
Before acting, confirm:
- What clinic or list of clinics is being evaluated?
- What region or province?
- Is this qualification, territory scanning, or outreach prep?

## Step 2: Read Context
- Check rules/brand-voice.md (always)
- Check memory/domain-state/prospect-filter.md for disqualification log and prior evaluations
- Check memory/feedback-log.md for recent corrections

## Target Specialties
All independent clinics that perform in-office procedures are in scope. This is the canonical specialty list — used for both qualification and as the scan order within each city in leads-progress.json.

**Dental**
- Dental (covers general, family, orthodontics, oral surgery, periodontics, endodontics, prosthodontics, pediatric dentistry)

**Medical — Primary Care**
- Family Medicine (GPs and family doctors with procedure suites)
- Pediatrics (in-office procedures)
- Internal Medicine (in-office procedures)
- Geriatrics (in-office procedures)

**Medical — Surgical / Procedural**
- OB/GYN (colposcopy, IUD, minor surgery, prenatal procedures)
- ENT / Otolaryngology (scopes, biopsies, ear procedures)
- Ophthalmology (injections, laser, minor surgery)
- Dermatology (biopsies, excisions, Mohs, laser, injections)
- Plastic Surgery / Cosmetic Surgery (in-office procedures)
- Orthopedics (joint injections, aspirations, minor procedures)
- General Surgery / Private Surgical (accredited day surgery facilities)
- Urology (cystoscopy, vasectomy, biopsies)
- Vascular Surgery (in-office procedures)
- Colorectal Surgery (in-office procedures)
- Podiatry / Chiropody (nail surgery, wound care, injections)
- Oral and Maxillofacial Surgery (standalone surgical practices)

**Medical — Diagnostic / Interventional**
- Gastroenterology (colonoscopy, endoscopy suites)
- Cardiology (ECG, stress tests, echocardiography, minor procedures)
- Respirology / Pulmonology (spirometry, bronchoscopy)
- Neurology (EMG, nerve conduction studies, Botox injections)
- Rheumatology (joint injections, infusions)
- Allergy / Immunology (allergy testing, immunotherapy injections)
- Pain Management (nerve blocks, epidurals, trigger point injections)
- Sports Medicine (PRP, prolotherapy, injections)
- Oncology / Infusion (independent infusion and chemotherapy suites)
- Wound Care (independent wound care clinics)
- Hematology (infusion clinics)

**Mental Health / Psychiatry**
- Psychiatry (TMS, ECT, ketamine infusion)
- Psychology / Mental Health (TMS clinics)

**Reproductive Health**
- Fertility / Reproductive Medicine (IVF, IUI, egg freezing)
- Midwifery (provinces where independent birth centres exist)

**Allied Health**
- Physiotherapy (dry needling, ultrasound, shockwave, manual therapy)
- Chiropractic (manipulation, soft tissue procedures)
- Naturopathy / Integrative Medicine (IV therapy, injections, procedures)
- Acupuncture / Traditional Chinese Medicine
- Occupational Therapy (in-office procedures)
- Speech-Language Pathology (in-office procedures)
- Massage Therapy (therapeutic procedures where regulated)

**Vision / Hearing**
- Optometry (punctal plugs, foreign body removal, in-office procedures)

**Aesthetics**
- Medical Aesthetics (Botox, fillers, laser, IPL, body contouring — physician-led or NP-led)

**Diagnostic / Imaging**
- Sleep Medicine (independent sleep study clinics)

**Out of scope — no sterilization requirement:**
- Audiology (hearing tests, wax removal — no reusable instruments requiring autoclave)
- Medical Imaging / Radiology (ultrasound/X-ray — no surgical instrument sterilization)
- Laboratory / Specimen Collection (specimen handling, not instrument sterilization)

Fail if the clinic does not perform in-office procedures or does not fall under one of the in-scope categories above. Do not qualify Audiology, DI, or Lab clinics.

## Scanning Order
- Province order (fixed): BC → AB → SK → MB → ON → QC → NB → NS → NL → YT → NVT
- Within each province: cities in alphabetical order
- BC cities (explicit list): Abbotsford, Burnaby, Campbell River, Chilliwack, Coquitlam, Delta, Fort St. John, Kamloops, Kelowna, Langley, Maple Ridge, Mission, Nanaimo, Nelson, New Westminster, North Vancouver, Penticton, Port Coquitlam, Port Moody, Prince George, Prince Rupert, Richmond, Surrey, Terrace, Vancouver, Vernon, Victoria, West Vancouver, White Rock, Williams Lake
- All other provinces: identify major cities alphabetically using best available knowledge
- Within each city: scan specialties in the order listed above, one specialty at a time
- Progress tracked in outputs/leads-progress.json as Province > City > Specialty
- Session target: 10 leads per run. If a city+specialty combo is exhausted before 10, advance to the next specialty in that city, then next city, then next province.

## Step 3: Execute
1. Read outputs/leads-progress.json — find the first Province > City > Specialty not marked `done` or `exhausted`. That is the session target.
2. Run each prospect through the five-point qualification filter in order:
   a. Specialty match — must be on the supported specialty list above and perform in-office procedures. Fail if outside scope.
   b. Size fit — independent clinic, 1-5 operatories/exam rooms, max 2-3 locations. Fail if chain or hospital.
   c. Vendor entanglement — check for Telus Health ecosystem involvement. INSTANT FAIL if yes. Log reason.
   d. Province coverage — must be a Canadian clinic (any province or territory). Fail if US-based or outside Canada.
   e. Tech readiness — has a website, uses some cloud tools, not entirely paper-based. Flag as "maybe" if unclear.
3. Assign a verdict for each prospect:
   - PASS: meets all five criteria → add to Plane Leads project (see below)
   - FAIL: fails any hard criterion → log to disqualification log with reason, do not proceed
   - MAYBE: passes hard criteria but tech readiness or size is unclear → flag ⚠️ FOUNDER DECISION NEEDED with specific concern
4. For PASS verdicts — add to Plane Leads project:
   - Project ID: d7729497-59ad-44a0-b19f-45068db55544
   - Default state: "Not Contacted" (state ID: 701a8bf2-c902-4816-9057-401019cb502d)
   - Work item title: [Clinic Name] — [Specialty] — [Province]
   - Description should include: city, specialty, address, website, why they passed, and any notes
   - Do NOT draft outreach — that requires founder approval
5. Update outputs/leads-progress.json — mark the current Province > City > Specialty as `done` or `exhausted`
6. Update memory/domain-state/prospect-filter.md:
   - Add passed prospects to Qualified Prospects table with Plane work item ID
   - Add failed prospects to Disqualification Log with reason
   - Note any MAYBE prospects for founder review

## Step 4: Quality Check
- [ ] Sounds like a human wrote it?
- [ ] Matches our voice? (check rules)
- [ ] Specific, not generic?
- [ ] No banned phrases? ("HIPAA compliant", "patient data", "chaos")
- [ ] Telus Health vendor entanglement checked?
- [ ] Province is one Cliniio has mapped?
- [ ] No outreach drafted for unqualified prospects?
