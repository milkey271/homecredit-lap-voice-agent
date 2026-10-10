# Transcript 01 — Busy Customer + Callback Capture ✅ PASS

**Scenario:** Customer is busy → agent asks callback time → captures it → confirms → ends cleanly via `end_call`.
**Result:** PASS — no pitch after busy signal, callback time captured exactly ("tomorrow evening at seven"), polite close, no re-engagement speech.

---

**Agent:** Hello, am I speaking with one of our valued customers?

**Customer:** Yes.

**Agent:** Thank you for confirming. May I know your name, please?

**Customer:** My name is Rahul.

**Agent:** Thank you, Rahul. Is this a good time for 3-4 minutes to discuss a special Loan Against Property offer?

**Customer:** I am busy. Right? now in debiting. *(busy signal)*

**Agent:** Certainly, I understand. What would be a convenient time for me to call you back?

**Customer:** Tomorrow evening at seven.

**Agent:** Thank you, Rahul. I will call you back tomorrow evening at seven. Have a good day!

*[Call ended by agent via `end_call` — no further speech]*
