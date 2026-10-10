# Test Results

All scenarios below were exercised against the published agent (`agent_3303ee74d704f2b7ad9793384d`, v1) via Retell playground completions with full dynamic variables. Every terminal branch returned exactly one closing message plus an `end_call` invocation (`call_ended: true`) with no post-goodbye speech.

| # | Scenario | Customer input | Expected | Result |
|---|----------|----------------|----------|--------|
| 1 | Happy path (all 7 pass) | Residential flat, sole owner, originals at home, ₹50L, salaried + bank, ₹1cr value, 10 yrs (incl. multi-fact turns) | Expert handoff + `end_call` | PASS |
| 2 | Agricultural property | “Agricultural land in my village” | Polite disqualify + `end_call` | PASS |
| 3 | Cash income | Self-employed, cash income | Disqualify + `end_call` | PASS |
| 4 | Missing originals | “Only photocopies, originals lost” | Disqualify + `end_call` | PASS |
| 5 | Tenure 2 years | “Just 2 years” | Disqualify + `end_call` | PASS |
| 6 | Tenure 20 years | “20 years please” | Disqualify + `end_call` | PASS |
| 7 | ₹90L request | “I need 90 lakhs” | Offer ₹75L alternative, keep call open | PASS |
| 8 | Decline ₹75L alternative | “Need 90L only” | Polite close + `end_call` | PASS |
| 9 | Existing property loan | “Already have a loan on this property” | Specialist message + `end_call`, no checklist | PASS |
| 10 | EMI reduction | “Want to reduce my EMI” | Specialist message + `end_call` | PASS |
| 11 | Busy customer | “Busy, in a meeting” | Ask callback time (capture + close verified on follow-up turn) | PASS |
| 12 | Out-of-order | “Residential, jointly owned, worth 1.2cr” | Ask documents next, no repeats | PASS |
| 13 | Correction | “Residential… actually agricultural” | Latest wins → disqualify + `end_call` | PASS |
| 14 | Refusal / DNC | “Not interested, do not call again” | Respectful close + `end_call` | PASS |
| 15 | Missing variables + rate question | Empty vars, “What interest rate?” | No placeholders spoken; rate → expert; back to checklist | PASS |
| 16 | Fixed greeting (no vars) | “Yes, this is Rahul.” | Personalizes (“Thank you, Rahul…”), no placeholders | PASS |

## How to reproduce (voice)

1. Open the published Retell agent → **Test Audio**.
2. Fill **Test Inputs → Dynamic Variables**: `company_name=Home Credit`, `customer_name=Rahul Sharma`, `agent_name=Priya`, `agent_gender=female`, `current_date/current_day/current_time`, `additional_context_from_rag=(empty)`, `language_to_speak=English` (or Hindi).
3. Talk through each scenario above; verify the closing line is followed by actual call termination with no re-engagement speech.
4. Call recordings + transcripts from Retell **Call History** serve as audio evidence (screen recording submitted separately).

## Honest limitations

- Above are prompt-logic simulations, not acoustic voice tests; voice-level proof (TTS/STT, Hindi turn, live `end_call` audio cut) comes from the recorded Test Audio calls.
- One early live web call spoke `{{...}}` placeholders because no variables were passed — fixed by the placeholder-free greeting + §13 fallbacks (test 15–16).
