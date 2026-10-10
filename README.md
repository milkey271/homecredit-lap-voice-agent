# Home Credit — Loan Against Property (LAP) AI Voice Agent

SalesAgents AI hiring assignment submission. Automated voice agent on **Retell AI** that calls existing Home Credit customers about a pre-approved Loan Against Property offer (up to ₹75 lakh) and conducts a preliminary 7-point eligibility check before handing qualified leads to a senior human loan expert.

## Live agent

| Field | Value |
|---|---|
| Agent | `HomeCredit-LAP-Qualifier-Priya` |
| Agent ID | `agent_3303ee74d704f2b7ad9793384d` |
| Platform | Retell AI (published) |
| LLM | `gpt-4.1-mini`, temperature 0 |
| Voice | `11labs-Monika` (Indian English, female, professional) |
| Languages | `en-IN`, `hi-IN` |
| Greeting (`begin_message`) | `Hello, am I speaking with one of our valued customers?` (placeholder-free) |
| Tools | `end_call` (all terminal branches) |
| Post-call extraction | `customer_verified`, `property_type`, `ownership_status`, `documents_available`, `loan_amount`, `occupation`, `income_mode`, `market_value`, `tenure_years`, `call_outcome`, `disqualify_reason` |

> Published Retell share link and screen-recording Drive link are submitted separately in the assignment form.

## How it works

1. **Greeting + verification** — confirms the right customer; wrong person → callback capture + end.
2. **Busy check** — busy → asks callback time → ends. Never pitches to a busy customer.
3. **Offer** — loyalty-framed LAP offer up to ₹75 lakh.
4. **Transfer switch** — existing property loan / EMI-reduction request → loan-transfer specialist message → end (no phone-transfer integration; message + `end_call` per assignment).
5. **7-point checklist** (first-missing-question algorithm, out-of-order answers remembered, latest correction wins, ambiguous answers clarified — never assumed).
6. **Immediate disqualification** on any failed rule (agricultural property, missing originals, cash income, tenure outside 3–15) → specific reason → `end_call`.
7. **>₹75 lakh requests** are NOT rejected — agent offers proceeding with ₹75 lakh; only a “no” ends the call.
8. **Handoff gate** — senior-expert callback only after all 7 items are answered with zero failures and zero transfer flags.

## Assignment rules implemented (unchanged)

- Residential / Commercial / Industrial → pass; **Agricultural → fail**
- Sole / Joint ownership → both pass
- Original property documents → required
- Loan amount ≤ ₹75,00,000 → pass; above → 75L alternative question
- Salaried / Self-employed → both pass; **Bank income required, Cash → fail**
- Market value → captured only, **no minimum threshold invented**
- Tenure **3–15 years** inclusive → pass; outside → fail
- Interest rates never quoted — senior loan expert provides exact rates
- All 11 required variables used: `company_name`, `customer_name`, `agent_name`, `agent_gender`, `current_date`, `current_day`, `current_time`, `additional_context_from_rag`, `language_to_speak`, `conversation_history`, `customer_utterance`

## Files

- `system-prompt.md` — exact live system prompt (13 sections) + runtime config
- `TEST_RESULTS.md` — scenario-by-scenario test evidence and how to reproduce
