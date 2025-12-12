# Requirements Elicitation Report
## Pricelock Feature - Advanced Reservation Payment Enhancement

**Document Type**: Requirements Elicitation Summary  
**Elicitation Method**: Requirements Interview  
**Source**: Product Manager (Kirill Sanakin)  
**Date**: December 5, 2025  
**Duration**: 43 minutes  
**Business Analyst**: Oleh Syzonov  
**Project**: Rail Ninja - Pricelock Feature

---

## 1. FEATURE OVERVIEW

### 1.1 Feature Definition

**Pricelock** is an optional add-on service to Advanced Reservation that enables customers to split payment into two installments over time, reducing upfront financial commitment for advance train ticket bookings.

**Relationship to Existing Features**:
- **Advanced Reservation** (current): Default service when tickets not yet available for sale; customer pays 100% upfront
- **Pricelock** (new): Optional enhancement allowing payment split; activated under same conditions as Advanced Reservation

### 1.2 Business Rules

**BR-01: Activation Trigger**
- Pricelock available when Advanced Reservation is active
- Based on search depth (booking far in advance)
- Independent of route, train, fare type, or carrier

**BR-02: Payment Structure**
- Two-payment model: Payment 1 (immediate) + Payment 2 (deferred)
- Payment 1 includes service fee
- Payment 2 due N days before departure date
- Total amount unchanged from current full-payment pricing

**BR-03: Optional Service**
- Advanced Reservation remains default
- Pricelock is user-selectable option
- User can choose full payment or split payment at checkout

---

## 2. FUNCTIONAL REQUIREMENTS

### 2.1 User Journey Requirements

**FR-01: Checkout Flow Integration**

**Requirement**: Integrate Pricelock selection into existing payment step without extending customer journey.

**Details**:
- Display at last checkout step (payment method selection)
- User sees two payment options:
  - Option A: Pay full amount now (current behavior)
  - Option B: Pricelock - Split payment
- Selection does not add steps to booking funnel
- Seamless user experience maintained

**Source**: Interview lines 93-94

---

**FR-02: Payment Breakdown Display**

**Requirement**: Show clear payment split breakdown when Pricelock selected.

**Display Elements**:
- Payment 1 amount: "Pay today: [amount]"
- Payment 2 amount: "Pay [N] days before departure: [amount]"
- Total amount (unchanged from full payment)
- Due date for Payment 2 (actual date displayed)

**Source**: Interview lines 91-92

---

**FR-03: Payment Method Selection**

**Requirement**: User selects payment method applicable to both payments.

**Supported Methods**:
- Credit/debit cards
- Apple Pay
- Google Pay
- PayPal
- All standard Rail Ninja payment methods (20+ options)

**Behavior**: Single payment method selection at checkout, same method applies to both payments.

**Source**: Interview lines 91-92

---

**FR-04: Frontend Payment Calculation**

**Requirement**: Calculate payment split on frontend without additional backend API calls.

**Implementation**:
- Service fee already available in search API response
- Frontend performs split calculation
- No performance impact (calculation on client side)
- No timeout concerns with external systems

**Source**: Interview lines 93-94

---

### 2.2 Personal Cabinet Requirements

**FR-05: View Unpaid Invoices**

**Requirement**: User can view pending Payment 2 in personal cabinet.

**Display Information**:
- Order number and route details
- Payment 1 status (paid, date, amount)
- Payment 2 status (pending, due date, amount)
- Clear indication of outstanding balance

**Source**: Interview lines 96-97

---

**FR-06: Manual Payment Capability**

**Requirement**: User can initiate Payment 2 at any time before due date (not restricted to scheduled date).

**Behavior**:
- "Pay Now" button visible for pending Payment 2
- User can pay early (before due date)
- Redirects to payment processing
- Standard payment flow applies

**Source**: Interview lines 96-97

---

### 2.3 Payment Processing Requirements

**FR-07: Payment State Handling**

**Requirement**: System handles three payment states with appropriate user visibility.

**States**:
1. **Success**: Payment confirmed immediately
2. **Processing**: Bank processing payment (asynchronous)
3. **Failed/Error**: Payment rejected

**User Visibility**:
- Errors displayed immediately with clear messaging
- Processing status shown for pending payments
- Status visible in personal cabinet for both Payment 1 and Payment 2

**Source**: Interview lines 102-103

---

### 2.4 Operational Requirements

**FR-08: Back-Office Order Visibility**

**Requirement**: Operations team can view order status including both payment stages.

**Visible Information**:
- Order identification (ID, customer details, route)
- Payment 1 details (status, date, amount, method)
- Payment 2 details (status, due date, amount)
- Overall order status
- Payment history for both transactions

**Source**: Interview lines 96, 107-108

---

## 3. NON-FUNCTIONAL REQUIREMENTS

### 3.1 Performance

**NFR-01: No Journey Extension**
- Pricelock option must not increase checkout time
- No additional steps in booking funnel
- Target: <500ms for frontend calculation

**Source**: Interview lines 93-94

---

### 3.2 Security

**NFR-02: PCI Compliance**
- Maintain existing PCI DSS compliance
- Follow current security standards for payment processing
- No storage of card details (existing policy continues)

**Source**: Rail Ninja existing security policy

---

### 3.3 Integration

**NFR-03: Payment Gateway Compatibility**
- Work with existing payment gateway(s)
- Support asynchronous payment processing
- Handle webhook callbacks for status updates

**Source**: Interview lines 102-103

---

## 4. SCOPE BOUNDARIES

### 4.1 In Scope - MVP

✅ Two-payment structure (Payment 1 + Payment 2)  
✅ Checkout flow integration (payment option selection)  
✅ Personal cabinet view and manual payment  
✅ Payment state handling (Success/Processing/Failed)  
✅ Back-office order visibility  
✅ Frontend payment split calculation  

### 4.2 Out of Scope - MVP

❌ Terms & Conditions legal text (regulatory details handled separately)  
❌ Internal backend status model design (proposed solution required)  
❌ Multiple payment methods per order (same method for both payments)  

**Source**: Interview lines 100-101, 107-108

---

## 5. REQUIREMENTS TRACEABILITY

| Req ID | Requirement | Source | Priority |
|--------|-------------|--------|----------|
| FR-01 | Checkout flow integration | Interview L93-94 | MUST |
| FR-02 | Payment breakdown display | Interview L91-92 | MUST |
| FR-03 | Payment method selection | Interview L91-92 | MUST |
| FR-04 | Frontend calculation | Interview L93-94 | MUST |
| FR-05 | View unpaid invoices | Interview L96-97 | MUST |
| FR-06 | Manual payment capability | Interview L96-97 | MUST |
| FR-07 | Payment state handling | Interview L102-103 | MUST |
| FR-08 | Back-office visibility | Interview L96, 107-108 | MUST |
| NFR-01 | No journey extension | Interview L93-94 | MUST |
| NFR-02 | PCI compliance | Existing policy | MUST |
| NFR-03 | Payment gateway compatibility | Interview L102-103 | MUST |

---

## 6. REQUIREMENTS GAPS & CLARIFICATIONS NEEDED

### 6.1 Parameters Not Specified

The following parameters were referenced but not defined during elicitation:

**G-01: Payment Split Formula**
- Referenced: Payment 1 includes service fee, Payment 2 is remainder
- Not specified: Exact split (percentage or fixed amounts)
- Impact: Affects payment breakdown display (FR-02)

**G-02: N Days Value**
- Referenced: Payment 2 due "N days before departure"
- Not specified: Actual N value (7 days? 14 days? 30 days?)
- Impact: Affects due date calculation and display (FR-02)

**G-03: Reminder System**
- Question asked: Should system send payment reminders?
- Response ambiguous: "да Нет" (unclear yes/no)
- Impact: May affect notification requirements scope

### 6.2 Scenarios Not Discussed

**G-04: Non-Payment Handling**
- What happens if Payment 2 not made by due date?
- Auto-cancellation? Grace period? Manual intervention?
- Impact: Affects operational flow and order status model

**G-05: Refund Policy**
- How does Pricelock affect refund scenarios?
- Is service fee (Payment 1) refundable if user cancels?
- Impact: Affects terms & conditions and user communication

**G-06: Order Status Model**
- What are specific order status states with two payments?
- How do statuses transition?
- Note: PM indicated this should be proposed solution (not extracted from interview)

---

## 7. DELIVERABLES REQUIRED (PART 2)

Based on interview guidance (lines 107-112):

### 7.1 Documentation Artifacts

1. **User Journey Diagram** (last checkout step only)
2. **Operational Flow Diagram** (propose own backend solution)
3. **High-Level Wireframes/Mockups** (last step focus)
4. **Feature Description** (for business stakeholders)
5. **Acceptance Criteria** (free form format)

### 7.2 Documentation Approach

**Audience Consideration**:
- Business stakeholder readability (non-technical)
- Technical team implementation detail (sufficient for development)
- Logical structure (no specific template provided intentionally)

**Format**:
- Concise and focused (avoid overwork)
- AI tool usage encouraged (document prompts used)

**Source**: Interview lines 107-118

---

## APPENDIX A: INTERVIEW CONTEXT

**Interview Structure**:
- Introduction & experience discussion (15 minutes)
- Feature requirements elicitation (25 minutes)
- Deliverables explanation (3 minutes)

**PM Communication Style**:
- Direct and practical
- Focused on functional requirements
- Avoided revealing internal technical details
- Encouraged independent problem-solving

**Company Context**:
- BA team: 17 people across multiple projects
- Standardized templates for SRD, User Stories, design tasks
- Distributed team with various stakeholder management styles

---

## APPENDIX B: ELICITATION METHOD NOTES

**Technique Used**: Semi-structured interview
- Open-ended questions to understand feature concept
- Clarifying questions on specific requirements
- Confirmation of understanding throughout
- Multiple touchpoints on ambiguous areas

**Elicitation Quality**:
- Core feature concept well understood
- User journey requirements clearly defined
- Operational visibility needs captured
- Technical constraints identified

**Areas for Follow-up**:
- Specific parameter values (split formula, N days)
- Edge case handling (non-payment, refunds)
- Reminder system scope clarification

---

---

# AUTHOR'S NOTES

*The following section contains analytical commentary, methodology notes, and considerations for the business analyst. This section is not part of the formal deliverable but provides context for the requirements analysis process.*

---

## AN-1. INTERVIEW TECHNIQUE ASSESSMENT

### Positive Aspects Demonstrated

**✅ Active Listening & Confirmation**
- Multiple instances of "Я понял" (I understood) showing comprehension (lines 95, 104)
- Repeated key information back to PM for validation
- Asked follow-up questions when points unclear

**✅ Clarifying Questions Asked**
- Line 92-93: Asked about usability requirements and potential timeout issues
- Line 96-97: Confirmed back-office visibility needs
- Line 101: Probed on risks and error handling
- Line 104: Returned to format requirements for clarity

**✅ Structured Approach**
- Requested expected format early (line 28)
- Asked about documentation standards (line 123)
- Confirmed deliverables scope before proceeding

**✅ Technical Awareness**
- Asked about API timeouts and external system dependencies
- Understood implications of frontend vs backend calculation
- Probed payment processing asynchronous behavior

### Areas for Improvement

**⚠️ Ambiguous Response Not Challenged**

**Critical Example - Line 97-98**:
```
Oleh: "Должны ли мы напоминать за какой-то период поездки?"
      ("Should we remind before some period of the trip?")

Kirill: "да Нет."
        ("yes No.")

[No follow-up question asked]
```

**What should have happened**: 
- "Извините, можете уточнить?" (Sorry, can you clarify?)
- "Это да или нет?" (Is that yes or no?)
- "Напоминания будут или не будут?" (Will there be reminders or not?)

**Lesson**: When PM gives contradictory or unclear answer, immediately ask for clarification rather than moving forward with ambiguity.

**⚠️ Critical Details Not Probed**

Parameters referenced but not specified:
- Payment split formula (what goes in Payment 1 vs Payment 2?)
- N value (how many days before departure?)
- Reminder timing (if in scope - when to send?)

**What could have been asked**:
- "Какой процент платим сейчас?" (What percentage do we pay now?)
- "За сколько дней до отправления второй платеж?" (How many days before departure is second payment?)
- "Если напоминания, то когда отправлять?" (If reminders, when to send?)

**Counterpoint**: Some gaps may be intentional - PM explicitly said "propose own solution" for backend design. Not all gaps represent elicitation failures.

---

## AN-2. REQUIREMENTS COMPLETENESS ANALYSIS

### High-Confidence Requirements (Ready for Design)

| Requirement Area | Confidence | Rationale |
|-----------------|-----------|-----------|
| Two-payment structure | ✅ HIGH | Explicitly described, core feature concept |
| Checkout flow integration | ✅ HIGH | "Seamless, no journey extension" emphasized |
| Frontend calculation | ✅ HIGH | Technical approach explicitly stated |
| Personal cabinet visibility | ✅ HIGH | Clear user needs articulated |
| Payment states | ✅ HIGH | Three states clearly defined |
| Back-office needs | ✅ HIGH | Operational visibility requirements clear |

### Medium-Confidence Requirements (Assumptions Needed)

| Requirement Area | Confidence | Reason for Uncertainty |
|-----------------|-----------|----------------------|
| Payment split formula | ⚠️ MEDIUM | Referenced but not quantified |
| N days value | ⚠️ MEDIUM | Mentioned generically ("N days") |
| Reminder system | ⚠️ MEDIUM | Ambiguous interview response |
| Payment method continuity | ⚠️ MEDIUM | Not explicitly discussed |

### Low-Confidence Requirements (Not Discussed)

| Requirement Area | Confidence | Gap Type |
|-----------------|-----------|----------|
| Non-payment handling | ❌ LOW | Scenario not explored |
| Refund policy specifics | ❌ LOW | Not discussed for Pricelock context |
| Grace period logic | ❌ LOW | Not mentioned |
| Order status model | ❌ N/A | Intentional gap (PM: "propose own") |

---

## AN-3. GAP ANALYSIS & RESOLUTION STRATEGY

### Critical Gaps (Blockers for Design)

**Gap #1: Payment Split Formula**
- **What's missing**: Exact amounts/percentages for Payment 1 vs Payment 2
- **Why it matters**: Cannot design payment breakdown display without values
- **Resolution**: Create assumption based on:
  - Service fee typically 10-15% of ticket price (from Rail Ninja reviews)
  - 20/80 split common in "pay later" services (Klarna, Afterpay)
  - Document assumption clearly, mark as configurable

**Gap #2: N Days Value**
- **What's missing**: Specific number of days before departure
- **Why it matters**: Affects reminder timing, grace period calculations, user messaging
- **Resolution**: Propose 14 days based on:
  - Industry standard (airlines/hotels: 14-30 days)
  - Carrier booking windows (typically 7-14 days before departure)
  - Balances user flexibility with operational safety

**Gap #3: Reminders Scope**
- **What's missing**: Clear yes/no on whether reminders are MVP
- **Why it matters**: Major feature scope impact (design, implementation, testing)
- **Context**: Interview response "да Нет" contradicts Tactiq notes showing "parametrizable reminders"
- **Resolution**: 
  - Tactiq notes likely represent post-interview clarification (more detailed)
  - Reminders critical for payment 2 success (reduce forgotten payments)
  - Include in MVP with assumption documented

**Gap #4: Non-Payment Handling**
- **What's missing**: What happens if Payment 2 not made
- **Why it matters**: Affects order lifecycle, operational procedures, user terms
- **Resolution**: Propose grace period model:
  - 3-day grace period after due date
  - Auto-cancel after grace expires
  - Service fee forfeited (consistent with current policy)

### Non-Critical Gaps (Workarounds Available)

**Gap #5: Order Status Model**
- **Status**: Intentional gap - PM wants proposed solution
- **Strategy**: Design comprehensive state machine based on:
  - Current Rail Ninja status patterns
  - Two-payment lifecycle requirements
  - Grace period and cancellation scenarios

**Gap #6: Refund Policy Details**
- **Status**: Not discussed, but existing policy provides guidance
- **Strategy**: Assume continuity with current policy:
  - Service fees non-refundable (Rail Ninja T&C)
  - Ticket portion refundable per fare rules

---

## AN-4. INTERVIEW METHODOLOGY NOTES

### Why This Interview Was Effective

**✅ Clear Feature Scope**
- PM provided assignment brief upfront (PDF file shared)
- Core concept explained clearly ("add-on to Advanced Reservation")
- Scope boundaries established (last checkout step only for flows)

**✅ Realistic Constraints**
- PM didn't reveal internal backend details (intentional)
- Forced candidate to propose solutions
- Simulates real BA work (incomplete information, reasoned assumptions)

**✅ Practical Guidance**
- Encouraged AI tool use
- Warned against overwork ("быстро коротко и по делу")
- Set clear deliverable expectations

### What Made Some Requirements Unclear

**Interview Dynamics**:
- 43-minute duration = time pressure
- Some questions answered briefly
- Technical vs business focus shifted throughout

**PM Strategy** (apparent):
- Left some gaps intentionally to see problem-solving approach
- Explicitly said "propose own solution" for backend design
- Testing candidate's ability to work with ambiguity

**Language Factor**:
- Interview in Russian, some responses culturally contextual
- "да Нет" could mean:
  - "Yes, no [not user-configurable]"
  - "Yes... actually no"
  - "Yes [we should remind], no [specific timing]"

---

## AN-5. COMPARISON: INTERVIEW vs TACTIQ vs WEBSITE

### Reminders Feature - Contradictory Information

| Source | Finding | Confidence |
|--------|---------|-----------|
| Interview | "да Нет" - ambiguous | LOW |
| Tactiq Notes | "Parametrizable reminders - system + user side" | MEDIUM |
| Website | Email notification infrastructure exists | HIGH (capability) |

**Resolution Logic**:
1. Tactiq notes more detailed than live interview → likely post-interview clarification
2. PM may have clarified after seeing candidate confusion
3. Reminders critical for "pay later" success → business case strong
4. **Decision**: Include reminders in MVP, document assumption

### Payment Split - Consistent Gap

| Source | Finding |
|--------|---------|
| Interview | "Service fee" in Payment 1, remainder in Payment 2 - no percentages |
| Tactiq Notes | Same - mentions split but no formula |
| Website | Service fee ~10-15% of ticket (from reviews) |

**Conclusion**: This is genuine requirements gap, not elicitation failure. PM didn't specify, likely configurable parameter.

---

## AN-6. QUALITY METRICS

### Requirements Elicitation Score

**Completeness**: 7/10
- Core requirements well captured
- Some critical parameters missing
- Intentional gaps (backend design) appropriate

**Clarity**: 8/10
- Most requirements clear and actionable
- Few ambiguous points documented
- Good use of specific examples

**Traceability**: 9/10
- All requirements linked to interview lines
- Clear source attribution
- Easy to verify against transcript

**Actionability**: 7/10
- Can proceed with design with assumptions
- Some decisions require business analyst judgment
- Acceptable for Part 2 progression

### Recommendations for Future Interviews

1. **Clarify ambiguous responses immediately** - don't proceed with "да Нет" type answers
2. **Ask for concrete examples** - "Can you give me example amounts for Payment 1 and 2?"
3. **Probe edge cases** - "What if Payment 2 isn't made?"
4. **Confirm numerical parameters** - "You mentioned N days - what's typical N value?"
5. **Summarize at intervals** - "Let me confirm what I heard..."

---

## AN-7. ELICITATION LESSONS LEARNED

### What Worked Well

**Preparation**:
- Reading assignment brief before interview
- Understanding company context (BA team structure, standards)
- Technical background enabled deeper questions

**During Interview**:
- Asked for format expectations early
- Confirmed understanding regularly
- Probed technical constraints
- Showed interest in company practices

**Post-Interview**:
- Documented gaps immediately
- Cross-referenced with other sources (Tactiq, website)
- Identified assumptions needed for progression

### What Could Improve

**During Interview**:
- Push back on ambiguous answers
- Ask for concrete examples more often
- Probe "what if" scenarios more deeply
- Request rough parameter ranges even if exact values unknown

**Questions to Add Next Time**:
- "Can you give me a typical example with actual amounts?"
- "What happens if [edge case]?"
- "Is there a range for [parameter]?"
- "Who decides [configurable item]?"

---

## AN-8. USING THIS DOCUMENT FOR PART 2

### For User Flow Diagram
**Use Section 2.1** (User Journey Requirements):
- FR-01: Checkout flow integration
- FR-02: Payment breakdown display
- FR-03: Payment method selection
- FR-06: Manual payment capability

**Cross-reference with**:
- Rail Ninja Web Analysis §2.2 (current payment step)
- Assumptions A1-A3 (concrete values)

### For Operational Flow
**Use Section 2.4** (Operational Requirements):
- FR-08: Back-office visibility

**Plus from Section 6**:
- G-04: Non-payment handling (propose solution)
- G-06: Order status model (propose solution)

**Cross-reference with**:
- Rail Ninja Web Analysis §4 (current order management)
- Assumptions A4, A6, A11 (operational logic)

### For Wireframes
**Use Section 2** (all Functional Requirements):
- Especially FR-02 (payment breakdown) and FR-05 (personal cabinet)

**Get concrete values from**:
- Assumptions Document (20/80 split, 14 days, etc.)

### For Feature Description
**Use Section 1** (Feature Overview):
- Business rules
- Relationship to Advanced Reservation

**Cross-reference with**:
- Assumptions Document §1 (critical assumptions to document)

### For Acceptance Criteria
**Use Section 2** (Functional Requirements):
- Convert each FR to Given-When-Then format
- Reference assumptions where needed

---

## AN-9. RISK ASSESSMENT

### High-Risk Areas (If Assumptions Wrong)

**Payment Split Formula (A1)**
- Risk: Wrong percentage → all wireframes show wrong amounts
- Mitigation: Label as "configurable" everywhere
- Impact: Medium (visual changes only)

**Non-Payment Handling (A4)**
- Risk: Wrong grace period logic → operational flow invalid
- Mitigation: Clearly mark as "proposed approach"
- Impact: High (affects order lifecycle)

**Reminders in MVP (A3)**
- Risk: If actually out of scope → extra work
- Mitigation: Design as modular feature
- Impact: Medium-High (scope creep if wrong)

### Medium-Risk Areas

**N Days Value (A2)**
- Risk: Wrong default → reminder timing off
- Mitigation: Use "N (configurable)" notation
- Impact: Medium (easy to adjust)

**Tickets Issuance Logic (A6)**
- Risk: Wrong dependency → business logic error
- Mitigation: Based on standard practice (low risk of being wrong)
- Impact: High if wrong (but unlikely)

### Low-Risk Areas

Most secondary assumptions (A8-A17) are based on:
- Industry standards
- Existing Rail Ninja policies
- Technical best practices

Even if slightly off, minimal design impact.

---

## AN-10. SUCCESS CRITERIA FOR PART 2

This elicitation is successful if Part 2 deliverables can be created with:

✅ **User Flow**: Complete journey through last checkout step with Pricelock  
✅ **Operational Flow**: Order lifecycle with both payment stages  
✅ **Wireframes**: Realistic UI mockups with actual values  
✅ **Feature Description**: Clear business and technical documentation  
✅ **Acceptance Criteria**: Testable scenarios covering main flows  

All while:
- ✅ Clearly documenting assumptions
- ✅ Flagging areas needing validation
- ✅ Maintaining professional quality
- ✅ Staying concise (per PM guidance)

---

## AN-11. DOCUMENT EVOLUTION NOTES

**Version History**:
- v0.1: Raw interview notes
- v0.5: Structured requirements with 37 questions
- v1.0: This document - professional requirements catalog with Author's Notes

**What Changed**:
- Moved meta-commentary to Author's Notes
- Main sections now deliverable-quality
- Cleaner separation of facts vs analysis

**Why This Structure**:
- Main sections can be included in final SRD
- Author's Notes show analytical thinking process
- Candidate can submit main sections, keep notes private

---

**End of Author's Notes**
