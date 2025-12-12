# Purpose
Artifacts in this repository showcase Business Analysis work on defining characteristics of new feature that is extension of payment plans on rail tickets trading platform. The target and main document is [SRD ](Software_Requirements_Document.md)

# Scope
- [Task Description](Task_Description.md)
- [BA Quality Goals](Document_Compliance_Mapping.md) - Analysis of Task and Industry Requirements
- [Requirements Elicitation Results](01_interview_elicitation_results.md)
- [Existing Solution Analysis](02_rail_ninja_web_analysis.md) (web-platform, mobile app)
# Limitations
1. This BA work is zero-budget, that lead to:
	1. **Inability to investigate Private Cabinet** due to that account creation requires ordering ticket(s)
	2. Limited choice of AI tools
	3. Limited in time and amount of requests and volume of data processed by AI 
2. The work had deadline in 1 week
3. [Assumptions](03_assumptions_and_decisions.md) made to mitigate limitations and knowledge gaps

# Result
- [Software Requirements Document](Software_Requirements_Document.md) - the main document
- UI Mock-ups - are referenced in BRD
	- [Checkout](Wireframe_1_Checkout_Pricelock.html)
	- [Pricelock Payment Breakdown](Wireframe_2_Pricelock_Breakdown.html)
	- [Payment Success Screen](Wireframe_3_Payment1_Success.html)
	- [Personal Cabinet](Wireframe_4_Personal_Cabinet.html)
	- [Payment Reminder](Wireframe_5_Email_Reminder.html)
- [Test Cases](Test_Cases_Pricelock.md) - extends use case referenced in the SRD with execution details
