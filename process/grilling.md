# Grilling — CLAUDE.md section 3.1

Mandatory at every pipeline level. Done at two points: **before stage 2 ends** and **before stage 3 starts**.

The goal is to close every decision that is **expensive to change later** before work begins. It is not to ask about everything.

## Steps

1. Read the requirement **in full** before asking. Ask only what the documents leave unanswered.
2. Look for these seven kinds, and turn them into questions:
   - **The real problem** — how is this work done today, by whom, where does it lose time or go wrong? Does the request fix that point, or is there an easier way for the person doing the work?
   - **Gaps** — things a real system needs that the document never mentions (cancelling a bill, a minimum age, decimals of a unit of measure).
   - **Ambiguity** — a statement that reads two ways with different results.
   - **Conflict** — two items that cannot both be done.
   - **Asymmetric cost** — free to decide now, a rewrite to change later (schema, data units, append-only records).
   - **Quality beyond function** — number of users and volume of data · the real devices and internet on site · permissions of each role · personal data · backup and restore.
   - **Law and regulation of the business** — licences, mandatory forms and reports, record-keeping periods, age or quantity limits, tax, personal-data law. Write what applies into `PROJECT.md` so every stage sees it.
3. **Order the questions by the cost of changing the answer later**, not by their order in the document.
4. Ask in batches of 3–7 per round, **each with your own proposal** and the reason for it. The human may answer "as you propose".
5. **Challenge an answer that will not work, with a worked example in real numbers.** Walk the case to show where it breaks, then propose a way that reaches the same result without breaking. An answer you know is broken never goes into a document unchallenged.
6. Finished when **every question on the list has an answer**, not when the human seems satisfied.

Ask in the human's language.

> This step removes more revision rounds than any other in the pipeline. A good grilling round cuts work out; it does not add work.
