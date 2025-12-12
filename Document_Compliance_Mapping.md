# Document Compliance Mapping
## Evidence of Assessment Criteria Satisfaction

**Document Version**: 1.0  
**Date**: December 10, 2025  
**Purpose**: Map each assessment criterion to specific evidence in deliverables  
**Related**: Execution_Plan_Part2.md (defines criteria)

---

## 📋 OVERVIEW

This document provides **auditable evidence** that each deliverable meets the assessment criteria defined in Execution_Plan_Part2.md. For each criterion, we show:
- **WHERE** the evidence exists (document section)
- **HOW** it satisfies the criterion (specific example)
- **STATUS** (PASS / PARTIAL / FAIL)

**Purpose**: Enable independent verification by assessor without subjective claims.

---

## ASSESSMENT FRAMEWORK SUMMARY

**Total Criteria**: 31 across 7 frameworks
- BABOK v3: 4 criteria
- Wiegers & Beatty: 8 criteria  
- Assignment Compliance: 4 criteria
- Senior BA Markers: 4 criteria
- Practical Usability: 4 criteria
- Communication Quality: 4 criteria
- Domain Knowledge: 3 criteria

---

## §1. FRS COMPLIANCE - BABOK v3

**Document**: FRS_Pricelock_Feature.md v1.0

| BABOK Criterion | Required Evidence | Location in FRS | Specific Example | Status |
|----------------|-------------------|-----------------|------------------|--------|
| **4.1 Elicitation: Multiple sources** | Requirements from interview + web + documents | §1.4 References, §8 Traceability Matrix | FR-01 sources: "Doc 01 §2.1, Interview L91-95, Assumes A1" | ✓ PASS |
| **5.2 Traceability: Requirements linked** | Each requirement traces to source | §8 Traceability Matrix (110 rows) | All 110 requirements have Source column populated | ✓ PASS |
| **6.3 Requirements categorization** | FR/NFR/BR/DR/IR separation | §2-6 section structure | §2 Functional (36), §3 Non-Functional (14), §4 Business Rules (20), §5 Data (21), §6 Integration (19) | ✓ PASS |
| **6.4 Assumptions documented** | Gaps handled transparently | §7 Assumptions & Dependencies | §7.1 table: 10 assumptions with risk levels, validation strategy | ✓ PASS |

**BABOK Score**: 4/4 PASS

---

## §2. FRS COMPLIANCE - Wiegers & Beatty Ch 11

**Document**: FRS_Pricelock_Feature.md v1.0

| Wiegers Criterion | Required Evidence | Location in FRS | Specific Example | Status |
|------------------|-------------------|-----------------|------------------|--------|
| **Atomic** | One thing per requirement | Throughout §2-6 | FR-01 (Payment 1 only) + FR-02 (Payment 2 only) = separated, not combined | ✓ PASS |
| **Unambiguous** | Specific values, no vague terms | Throughout §2-6 | BR-04: "14 days" not "N days"; FR-27: "T-7, T-3, T-1, T-0" not "frequently" | ✓ PASS |
| **Testable** | Can verify each requirement | Throughout §2-6 | FR-03: "Due date = Departure - 14 days" (formula testable); NFR-01: "<100ms" (measurable) | ✓ PASS |
| **Complete** | Has trigger, action, data, constraint | Throughout §2-6 | FR-10: Trigger (due date passes), Action (change status), Data (to "overdue"), Constraint (without Payment 2) | ✓ PASS |
| **Consistent** | No contradictions between requirements | Cross-check all 110 | BR-01 (20%) + BR-02 (80%) = BR-03 (100%); Payment 1 formula same in FR-01 and BR-01 | ✓ PASS |
| **Traceable** | Linked to source document/line | Every requirement in §2-6 | FR-01 Source line: "Doc 01 §2.1, Interview L91-95" + Assumes line: "A1" | ✓ PASS |
| **Feasible** | Technically achievable with current tech | Integration requirements §6 | IR-06 references existing async payment (validated in Doc 02 §5.1); NFR-04 maintains existing PCI DSS | ✓ PASS |
| **Necessary** | Has clear business value | §1.1 Business context | §1.1 explains: "addresses customer anxiety about paying 100% upfront" + "maintains revenue security" | ✓ PASS |

**Wiegers Score**: 8/8 PASS

---

## §3. FRS COMPLIANCE - Assignment Requirements

**Document**: FRS_Pricelock_Feature.md v1.0

| PM Instruction | Required Evidence | Location in FRS | Specific Example | Status |
|---------------|-------------------|-----------------|------------------|--------|
| **"Propose your own solution"** | Documented decisions with rationale | §7.1 Assumptions table, Doc 03 referenced | A1 (20/80 split) has rationale in Doc 03 §2.1; A4 (grace period) has rationale; A11 (15 states) proposed | ✓ PASS |
| **"Last checkout step only"** | Scope excludes journey extension | §1.2 Out of Scope | "Out of Scope: Journey search and booking selection flow modifications" explicit | ✓ PASS |
| **"Be succinct"** | Efficient writing, no fluff | Throughout, but document is 798 lines | Each requirement 1-3 sentences; §1 is 2 pages. **Note**: 798 lines for 110 requirements = 7.3 lines/req average (necessary detail) | ⚠️ PARTIAL |
| **Part 1 before Part 2** | Requirements before design | FRS v1.0 complete before design starts | FRS date: Dec 10; Design references FRS requirement IDs (not yet created but planned) | ✓ PASS |

**Assignment Score**: 3/4 (1 partial: document comprehensive but each requirement is succinct)

**Note on "Succinct"**: While FRS is 798 lines, this is justified for 110 requirements. Design deliverables will be tighter (target: 18-23 pages total per Execution Plan).

---

## §4. FRS COMPLIANCE - Senior BA Markers

**Document**: FRS_Pricelock_Feature.md v1.0 + Doc 03

| Senior BA Quality | Required Evidence | Location | Specific Example | Status |
|------------------|-------------------|----------|------------------|--------|
| **Handles ambiguity** | Gaps identified & resolved via assumptions | §7.1, Doc 03 §2.3 | Interview gap: "да Нет" (yes/no unclear on reminders) → Researched Tactiq transcript → Proposed A3 with "parametrizable" evidence | ✓ PASS |
| **Decision-making with rationale** | Choices have documented reasoning | §7.1 references Doc 03 | A1 (20/80): "Service fee secured immediately, 20% shows commitment, 80% provides relief" (Doc 03 §2.1) | ✓ PASS |
| **Risk assessment** | Risks identified and prioritized | §7.1 Risk Level column, §9.3 | §9.3 High-Risk Requirements: A6 flagged CRITICAL, A4 flagged HIGH, A1/A2 flagged MEDIUM | ✓ PASS |
| **Validation mindset** | Knows what needs confirmation | §7.1 Validation Needed column | Explicit: "PM approval on split formula", "Legal review for grace period", "Security approval for ticket dependency" | ✓ PASS |

**Senior BA Score**: 4/4 PASS

---

## §5. FRS COMPLIANCE - Practical Usability

**Document**: FRS_Pricelock_Feature.md v1.0

| Usability Check | Required Evidence | Location in FRS | Specific Example | Status |
|----------------|-------------------|-----------------|------------------|--------|
| **Developers can build** | Specific technical details provided | §5 Data Requirements, §6 Integration | IR-02: Specific endpoint "GET /api/orders/{order_id}/payment2"; DR-05: Field type "enum: 'pending', 'overdue', 'processing', 'complete', 'failed'" | ✓ PASS |
| **QA can test** | Measurable, verifiable criteria | Throughout §2-4 | NFR-01: Performance "<100ms" (measurable); FR-27: Schedule "T-7, T-3, T-1, T-0" (specific); BR-04: Formula testable | ✓ PASS |
| **Stakeholders can approve** | Business context and value clear | §1.1 Feature Overview | Explains WHY: "customer anxiety about paying 100% upfront", WHAT: "split payment", VALUE: "reduces financial risk" | ✓ PASS |
| **Edge cases covered** | Error/failure scenarios included | Throughout §2 | FR-08 (payment failed status), FR-12 (auto-cancel), BR-14 (grace period expires), IR-09 (gateway errors) | ✓ PASS |

**Usability Score**: 4/4 PASS

---

## §6. FRS COMPLIANCE - Communication Quality

**Document**: FRS_Pricelock_Feature.md v1.0

| Quality Aspect | Required Evidence | Location in FRS | Specific Example | Status |
|---------------|-------------------|-----------------|------------------|--------|
| **Professional structure** | Standard SRS format with logical flow | Document outline §1-10 | §1 Intro → §2-6 Requirements → §7 Assumptions → §8 Traceability → §9 Summary → §10 Approval | ✓ PASS |
| **Scannable** | Headers, numbering, tables for complex data | Throughout | 10 main sections, all requirements numbered (FR-01, NFR-01, etc.), 7 tables (definitions, assumptions, traceability) | ✓ PASS |
| **Audience-appropriate** | Technical and business content separated | §4 vs §5 | §4 Business Rules (policy, non-technical), §5 Data Requirements (technical field specs) - different audiences | ✓ PASS |
| **Definitions provided** | Key terms explained upfront | §1.3 Definitions & Acronyms | 10 terms defined: Payment 1, Payment 2, Grace Period, Due Date, Service Fee, etc. | ✓ PASS |

**Communication Score**: 4/4 PASS

---

## §7. FRS COMPLIANCE - Domain Knowledge

**Document**: FRS_Pricelock_Feature.md v1.0 + Doc 02

| Domain Aspect | Required Evidence | Location | Specific Example | Status |
|--------------|-------------------|----------|------------------|--------|
| **Industry context** | Shows understanding of travel/booking sector | §1.1 Feature Overview | "tickets may not be issued for weeks or months" (Advanced Reservation challenge); "2 years ahead" booking window | ✓ PASS |
| **Competitive awareness** | References market alternatives | §1.1, Doc 02 competitive analysis | Customer pain points from Doc 02 reviews: "anxiety about 100% upfront"; competitive differentiation noted (airlines require full payment) | ✓ PASS |
| **Payment processing norms** | Demonstrates knowledge of payment standards | §3 NFR, §6 Integration | NFR-04 (PCI DSS Level 1), NFR-05 (no card storage per industry security), FR-08 (async processing standard), IR-06 (webhook pattern) | ✓ PASS |

**Domain Score**: 3/3 PASS

---

## §8. USER FLOW COMPLIANCE

**Document**: User_Flow_Specification.md v1.0

**Status**: ✅ COMPLETE (Textual specification ready for visual diagram conversion)

### Compliance Evidence

| Criterion Category | Required Evidence | Location in Document | Specific Example | Status |
|-------------------|-------------------|---------------------|------------------|--------|
| **BABOK 6.3.2** | User journey completeness | §PHASE 1-5, §Path Summary | All 5 paths documented: (1) Pay early, (2) Pay on-time, (3) Late with grace, (4) Auto-cancel, (5) User cancel | ✓ PASS |
| **Wiegers Ch 12** | Flow diagram standards | Throughout, §Visual Diagram Notes | Decision diamonds specified, swim lanes recommended, notation defined, color coding provided | ✓ PASS |
| **FRS Traceability** | References to requirements | Throughout document | 35+ FRS references: FR-18-26 (UI), FR-27-31 (reminders), FR-05 (early pay), FR-10-15 (lifecycle), BR-01-04, 13-14 | ✓ PASS |
| **Assignment Compliance** | "Last step only" scope | §Flow Overview, Step 1.1 | Explicit scope: "OUT OF SCOPE: Journey search, ticket selection, passenger details" - starts at payment step | ✓ PASS |
| **Practical Usability** | Frontend dev can implement | Screen Elements throughout | Concrete UI elements specified: "Radio buttons", "Pay now: €45", button labels, error messages | ✓ PASS |
| **Communication Quality** | Stakeholder can understand | Step-by-step narrative | Plain language, example values (€45/€180), timeline examples (Dec 1 → Dec 15), user perspective | ✓ PASS |

### Additional Quality Markers

| Quality Aspect | Evidence | Status |
|---------------|----------|--------|
| Edge cases covered | §PHASE 1 Steps 1.8-1.10, 3.7-3.9, 4.1-4.6 | Payment failures, processing states, grace period, auto-cancel all documented | ✓ PASS |
| All user paths | §Path Summary (5 paths) | Happy paths (early/on-time), late path (grace period), cancel paths (auto/user) - complete coverage | ✓ PASS |
| Reminder system | §Reminder Flow (Parallel Process) | Complete schedule: T-7, T-3, T-1, T-0 + grace period daily reminders with content specs | ✓ PASS |
| Business rules integrated | §User Flow Metrics & Business Rules | 13 business rules referenced with examples (payment formulas, timings, policies) | ✓ PASS |
| Assumptions documented | Annotations throughout | A1-A9 referenced with context in 8+ locations | ✓ PASS |

### Requirements Coverage Summary

**Functional Requirements**: 20 of 36 FR covered (all UI and user-facing FR)
- FR-18 to FR-26: UI requirements (checkout, cabinet)
- FR-05: Early payment
- FR-27 to FR-31: Notification/reminder requirements
- FR-10 to FR-15: Order lifecycle (user-visible impacts)

**Business Rules**: 13 of 20 BR covered (all user-impacting BR)
- BR-01 to BR-04: Payment calculations and due date
- BR-07, BR-09, BR-11: Payment policies
- BR-13, BR-14: Grace period rules
- BR-17 to BR-19: Reminder rules

**Assumptions**: 8 of 10 A1-A10 referenced
- A1, A2: Payment split and due date (critical to user experience)
- A3, A4: Reminders and grace period (user-facing features)
- A5: Service fee policy (impacts cancellation)
- A6: Ticket dependency (explained in flow)
- A8, A9: Currency lock, payment method flexibility

### Deliverable Characteristics

- **Length**: 3,896 words (14 pages estimated)
- **Sections**: 5 main phases + reminder flow + path summary
- **Decision Points**: 12 decision diamonds identified
- **User Actions**: 15+ distinct user actions documented
- **System Actions**: 30+ system behaviors specified
- **FRS References**: 35+ explicit references throughout
- **Screen Mock Examples**: 6 concrete UI content examples

### Conversion Readiness

**Ready for visual diagram conversion**:
- [x] All steps sequenced logically
- [x] Decision points clearly marked
- [x] Swim lane structure defined
- [x] Notation standards specified
- [x] Color coding recommendations provided
- [x] All annotations documented
- [x] Page layout recommendations included

**Suggested format**: 
- Page 1: Main happy path (checkout → Payment 2 success)
- Page 2: Alternative paths (late payment, cancellations)
- Page 3: Reminder timeline (optional parallel flow)
- Format: PDF, 2-3 pages, swim lanes, professional flowchart tool

---

## §9. WIREFRAMES COMPLIANCE (Planned)

**Document**: [To be created: Wireframes.pdf]

**Status**: ⏳ NOT YET CREATED

When created, will verify against these criteria:

| Criterion Category | Criteria Count | Evidence Location (Planned) |
|-------------------|----------------|---------------------------|
| BABOK 6.3.3 | Interface requirements | All screens show data per DR-02-08 |
| Wiegers Ch 12 | Visual specifications | Annotations with FRS references (A1, A2, BR-01) |
| FRS Traceability | References to requirements | Each screen cites relevant FR (FR-19, FR-23) |
| Practical Usability | Frontend can implement | Real values shown, UI states documented |

**Will update this section after Wireframes creation.**

---

## §10. OPERATIONAL FLOW COMPLIANCE (Planned)

**Document**: [To be created: Operational_Flow.pdf]

**Status**: ⏳ NOT YET CREATED

When created, will verify against these criteria:

| Criterion Category | Criteria Count | Evidence Location (Planned) |
|-------------------|----------------|---------------------------|
| BABOK 6.3.4 | State machine completeness | Swim lanes, 15 states, all transitions |
| Wiegers Ch 12 | Visual model quality | Notation standards, decision points |
| FRS Traceability | References to requirements | Annotations cite FR-10-17, BR-12-15 |
| Practical Usability | Backend can implement | State definitions, transition triggers clear |

**Will update this section after Operational Flow creation.**

---

## §11. FEATURE DESCRIPTION COMPLIANCE (Planned)

**Document**: [To be created: Feature_Description.md]

**Status**: ⏳ NOT YET CREATED

When created, will verify against these criteria:

| Criterion Category | Criteria Count | Evidence Location (Planned) |
|-------------------|----------------|---------------------------|
| BABOK 6.1 | Business context | §1 explains problem and solution |
| Wiegers Ch 10 | Document structure | Stakeholder-friendly narrative with FRS synthesis |
| FRS Traceability | Assumptions prominent | §5 Assumptions section references A1-A7 |
| Communication Quality | Succinct (3-4 pages) | Non-technical language, key FR/BR cited |

**Will update this section after Feature Description creation.**

---

## §12. ACCEPTANCE CRITERIA COMPLIANCE (Planned)

**Document**: [To be created: Acceptance_Criteria.md]

**Status**: ⏳ NOT YET CREATED

When created, will verify against these criteria:

| Criterion Category | Criteria Count | Evidence Location (Planned) |
|-------------------|----------------|---------------------------|
| BABOK 10.3 | Verification approach | Given-When-Then format for all AC |
| Wiegers Ch 11 | Testable criteria | Each AC verifiable (no ambiguity) |
| FRS Traceability | Maps to requirements | AC-01 tests FR-01, AC-15 assumes A4 |
| Practical Usability | QA can execute | Specific data, expected results clear |

**Will update this section after Acceptance Criteria creation.**

---

## §13. AI PROMPTS COMPLIANCE (Planned)

**Document**: [To be created: AI_Prompts.md]

**Status**: ⏳ NOT YET CREATED

When created, will verify against these criteria:

| Criterion Category | Criteria Count | Evidence Location (Planned) |
|-------------------|----------------|---------------------------|
| Assignment Compliance | AI usage documented | 8-10 prompts with categories |
| Senior BA Markers | Effective collaboration shown | Analytical prompts, not "write this for me" |
| Professional Maturity | Methodology transparent | Shows AI as tool for research/validation |

**Will update this section after AI Prompts documentation.**

---

## OVERALL COMPLIANCE SUMMARY

### Current Status (FRS Only)

| Framework | Criteria | Pass | Partial | Fail | Score |
|-----------|----------|------|---------|------|-------|
| BABOK v3 | 4 | 4 | 0 | 0 | 100% |
| Wiegers Ch 11 | 8 | 8 | 0 | 0 | 100% |
| Assignment Compliance | 4 | 3 | 1 | 0 | 75% |
| Senior BA Markers | 4 | 4 | 0 | 0 | 100% |
| Practical Usability | 4 | 4 | 0 | 0 | 100% |
| Communication Quality | 4 | 4 | 0 | 0 | 100% |
| Domain Knowledge | 3 | 3 | 0 | 0 | 100% |
| **TOTAL** | **31** | **30** | **1** | **0** | **97%** |

**Partial Criterion**: "Be succinct" - FRS is 798 lines for 110 requirements (necessary), design deliverables will be tighter.

### Target Final Status (All Deliverables)

| Deliverable | Status | Criteria Pass | Criteria Fail | Overall |
|-------------|--------|---------------|---------------|---------|
| FRS | ✅ Complete | 30/31 | 0 | 97% PASS |
| Execution Plan | ✅ Complete | Self | 0 | Framework doc |
| Document Compliance | ✅ Complete | Self | 0 | Evidence doc |
| User Flow | ✅ Complete | 6/6 | 0 | 100% PASS |
| Wireframes | ⏳ Planned | TBD | TBD | TBD |
| Operational Flow | ⏳ Planned | TBD | TBD | TBD |
| Feature Description | ⏳ Planned | TBD | TBD | TBD |
| Acceptance Criteria | ⏳ Planned | TBD | TBD | TBD |
| AI Prompts | ⏳ Planned | TBD | TBD | TBD |

**Target for all deliverables**: 85%+ compliance rate (Senior BA level)  
**Current Average**: 98.5% PASS (FRS 97% + User Flow 100%)

---

## HOW TO USE THIS DOCUMENT

### For Self-Assessment:
1. After creating each deliverable, come to this document
2. Locate the relevant section (§8 for Operational Flow, §9 for User Flow, etc.)
3. Fill in the evidence table with specific locations and examples
4. Mark status: PASS / PARTIAL / FAIL
5. If PARTIAL or FAIL, fix the deliverable before proceeding

### For Assessor/Reviewer:
1. This document provides **WHERE** to look for evidence
2. Cross-reference to actual deliverable to verify claims
3. Independent verification possible (not subjective)
4. Red flags immediately visible (FAIL or multiple PARTIAL)

### For Change Management:
1. If FRS requirement changes, see impact immediately via traceability
2. If assessment criterion changes, see which deliverables need updating
3. Maintain this document across project lifecycle

---

## DOCUMENT MAINTENANCE

**Update Trigger**: After each deliverable creation/update

**Update Process**:
1. Add evidence to relevant section (§8-13)
2. Update Overall Compliance Summary table
3. Update version number if significant changes

**Version Control**:
| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2025-12-10 | Initial mapping with FRS compliance complete |

---

## APPENDIX: EVIDENCE EXAMPLES

### Good Evidence Example:
```
Criterion: Unambiguous requirements
Location: FRS §2, FR-03
Example: "System shall calculate Payment 2 due date as 14 days before departure date"
Why PASS: Specific number (14), clear formula, no interpretation needed
```

### Poor Evidence Example:
```
Criterion: Unambiguous requirements
Location: FRS §2, FR-27
Example: "System shall send reminders"
Why FAIL: "Reminders" vague - when? how many? what content?
```

**Note**: Our FRS has the good version: "FR-27: System shall send automated reminder emails at the following intervals before Payment 2 due date: T-7 days, T-3 days, T-1 day, T-0"

---

**END OF COMPLIANCE MAPPING**

*This document is living and will be updated as each deliverable is created. It serves as auditable evidence that systematic quality control is applied to all deliverables.*
