# Teaching Method: How to Explain Security to a True Beginner

This file answers one question: for the same knowledge point, how do you write it so that someone with no background
**genuinely understands** it and **can actually use it**.

## Contents
1. Five rules of Feynman-style writing
2. Every step needs a why: the three questions
3. Explaining principles: start from the root cause
4. Breaking down commands and payloads
5. How to choose an analogy
6. Turning knowledge into "vulnerability intuition"
7. Common writing traps

---

## 1. Five rules of Feynman-style writing

1. **Assume the reader is smart but has zero background.** Never say "obviously" or "as we all know"; never assume they
   know an acronym.
2. **Conclusion first, details after.** Open every subsection with one sentence saying what it solves.
3. **Introduce a concept once and explain it immediately.** Keep the English term (Payload, Web Shell); explain its
   meaning in the local language the first time, then use it directly.
4. **Use an analogy when you can, then land on the technical detail.** The analogy builds the mental picture; the
   technical description provides precision. You need both.
5. **It must be repeatable when finished.** After writing a point, ask yourself: can a beginner close the notes and
   explain in their own words "what it is, why, how to do it"? If not, it is not written through yet.

## 2. Every step needs a why: the three questions

Every action in a penetration test exists to answer some question or rule out some possibility. In the notes, every step
answers these fixed items:

| Question | What to make clear |
| --- | --- |
| What to do | The concrete action, specific enough to follow |
| Why do it | The purpose: which hypothesis it verifies, which possibility it rules out, what it prepares for the next step |
| What you get | The expected observation; **what it means if you do not get it**, and how to adjust next |

Example: explaining "append a single quote to the parameter first" in SQL Injection.

- What to do: append `'` after the parameter value.
- Why: the single quote is the delimiter of a SQL string. If the input is concatenated directly into the query, the extra
  quote breaks the statement's syntax — this **probes whether user input is being treated as part of the code**.
- What you get: if the page errors or returns something abnormal, the input reached the SQL statement and is worth
  pursuing; if the page does not change at all, that does **not** mean there is no injection — errors may be suppressed,
  so switch to blind injection techniques to verify.

Writing only "add a single quote and see whether it errors" is the wrong approach: the beginner still does not know
**why**, and will not be able to use it in a different scenario.

## 3. Explaining principles: start from the root cause

Vulnerabilities are usually the same class of mistake: **the program treats "data" as "instructions"**, or **trusts
something it should not trust**. Follow this line when explaining the principle:

1. How the program normally works (the normal flow).
2. What assumption the developer made, and where (e.g. "the user will only enter numbers").
3. How an attacker breaks that assumption.
4. What consequence follows.

Only when the reader grasps the root cause can they recognize the same class of problem in a scenario they have never
seen. That is where "vulnerability intuition" comes from, and it is the part of the notes most worth the space.

## 4. Breaking down commands and payloads

Any command, parameter, or payload must be taken apart and explained. Format:

| Fragment | What it does | Why it is needed |
| --- | --- | --- |

Plus three more things:

- **What normal output looks like**, and which line holds the key information.
- **Which parameters are mandatory and which can be changed per scenario**, and on what basis you change them.
- **Where this command sits in the overall flow**: which step consumes its output.

## 5. How to choose an analogy

- Pick things the reader encounters daily: door access control, package delivery, a bank counter, ordering at a
  restaurant.
- The analogy must **map onto the key mechanism**, not merely be amusing. For example: "SQL concatenation is like copying
  a customer's spoken words straight into the order system — if the customer says 'and add one more order, free', the
  system copies and executes that too."
- After the analogy, explicitly point out **where the analogy differs from reality**, so it does not mislead.

## 6. Turning knowledge into "vulnerability intuition"

In the "how to use it in practice" section, build these three abilities in the reader:

- **Trigger cues**: what feature should make you think of this vulnerability (parameter concatenation, user-controlled
  URL, uploadable file types, exposed version numbers...).
- **Minimal verification**: confirm the hypothesis at the lowest cost and with the least disturbance to the target.
- **Decision branch**: what to do if it holds, what line of thinking to switch to if it does not.

Also write out the **shared pattern across this class of problem** where possible — e.g. "anywhere the server fetches an
address on the user's behalf, think SSRF" — so the reader can generalize.

## 7. Common writing traps

| Trap | Why it is bad | Fix |
| --- | --- | --- |
| Listing steps with no reasons | The reader can only memorize; useless in a new scenario | Add the three questions to every step |
| Stacking terms without explaining | Beginners give up | Explain fully on first appearance, keep the English term |
| Vague cases ("some company was attacked") | Cannot connect to business | Use a verifiable real incident, or a clearly labeled example scenario |
| Mixing added content into the original notes | The reader cannot verify anything | Use the "🔎 Added" callout |
| Long but without focus | Key points get buried | Use relevance rating to control depth |
| Repeating "authorized only" in every paragraph | Breaks the reading flow | Write it once at the top |
