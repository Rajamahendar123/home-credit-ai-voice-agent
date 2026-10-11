# Home Credit AI Voice Agent (Loan Against Property)

An outbound AI Voice Agent built on Retell AI for Home Credit to screen existing customers for a pre-approved Loan Against Property (LAP) offer up to ₹75 Lakhs.

---

## Architecture & System Design
- **Platform:** Retell AI
- **Conversation Pattern:** Extraction-First State Machine
- **Key Capabilities:**
  - **Dynamic Entity Extraction:** Extracts multiple parameters from compound utterances without forcing rigid linear Q&A.
  - **Deduplication:** Prevents re-asking previously supplied attributes.
  - **Deterministic Filtering:** Early termination for ineligible conditions (agricultural property, cash income, tenure outside 3–15 years, missing original documents).
  - **Specialist Escalation:** Direct handoff for existing loans / EMI reductions without questionnaire execution.
  - **Handoff Guardrail:** Only transfers to senior loan experts after all 7 mandatory parameters pass verification.

---

## 7 Eligibility Checkpoints
1. **Property Type:** Residential, Commercial, Industrial eligible. (Agricultural disqualified).
2. **Ownership:** Sole & Joint ownership eligible.
3. **Documents:** Original documents mandatory. (Photocopies disqualified).
4. **Loan Amount:** Capped at ₹75,00,000.
5. **Income Mode:** Salaried / Self-employed allowed via Bank transfer. (Cash disqualified).
6. **Market Value:** Estimated market value captured.
7. **Tenure:** 3 to 15 years allowed.

---

## Test Scenarios & Transcripts

### Scenario 1: Qualified Customer (Out-of-Order Extraction)
- **Agent:** Hello, am I speaking with Mr. Rahul?
- **Customer:** Yes, this is Rahul. What is this call regarding?
- **Agent:** We're reaching out because you've been pre-approved for a Loan Against Property of up to 75 lakh rupees based on your relationship with us. I just need to confirm a few quick details to see if this matches what you need.
- **Customer:** I have a residential house worth about 1.2 crore, and it's jointly owned with my wife. I'm looking for a loan of 50 lakhs.
- **Agent:** Got it. Do you have the original property documents available for physical verification?
- **Customer:** Yes, original documents are available at home.
- **Agent:** Great. Could you share your employment status and how you receive your income?
- **Customer:** I'm salaried, and my monthly salary is credited directly to my bank account.
- **Agent:** Understood. And what loan tenure are you looking for?
- **Customer:** Around 10 years.
- **Agent:** Thank you for sharing those details, Mr. Rahul. Everything meets our initial criteria. I'll pass your details to our senior loan expert, who will call you shortly to discuss the exact interest rates and documentation.
- **Result:** Successful human handoff.

---

### Scenario 2: Immediate Disqualification (Agricultural Land & Cash Income)
- **Agent:** Hello, am I speaking with Mr. Rahul?
- **Customer:** Yes, Rahul here. Tell me what this is about.
- **Agent:** We're reaching out because you've been pre-approved for a Loan Against Property of up to 75 lakh rupees based on your relationship with us. I just need to confirm a few quick details to see if this matches what you need.
- **Customer:** The property is agricultural farmland, and I receive my business income in cash.
- **Agent:** I understand, but unfortunately, agricultural properties and cash-based income are not eligible under this specific scheme. Thank you for your time, Mr. Rahul, and have a good day.
- **Result:** Early termination without redundant questioning.

---

### Scenario 3: Balance Transfer / Existing Loan
- **Agent:** Hello, am I speaking with Mr. Rahul?
- **Customer:** Yes, this is Rahul. I already have an ongoing loan on this property and want to reduce my EMI.
- **Agent:** Understood. Since you already have an active loan on the property, our balance transfer desk handles those cases. I'll arrange for a transfer specialist to get in touch with you shortly. Thank you for your time.
- **Result:** Redirected to balance transfer desk.
