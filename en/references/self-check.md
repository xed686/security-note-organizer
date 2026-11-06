# Pre-Delivery Self-Check

Go through every item after drafting. If any item fails, fix it before delivering.

## A. Reader's view (can a beginner understand it)
- [ ] Pick a random knowledge point: could someone with no security background explain "what it is, why, how to do it" in their own words after reading?
- [ ] Is the meaning of every term explained in the local language on first appearance, while the English term itself is kept?
- [ ] Does every key concept have at least one analogy, and does that analogy map onto the real mechanism?
- [ ] Any wording that assumes prior knowledge, such as "obviously" or "as we all know"?

## B. Thoroughness (principle, reasoning, procedure)
- [ ] Does every 🔴 point have a "why it exists (root cause)"?
- [ ] Does every step answer "what to do / why / what you get / what failure means"?
- [ ] Is every command or payload broken into fragments, with an explanation of how to read normal output?
- [ ] Are the notes just a "step list" with no why? (If so, add it)

## C. Business-anchored and practical
- [ ] Does every 🔴 point have a case (a real incident, or one labeled "example scenario")?
- [ ] Does each case cover all four things: what happened / root cause matching which link / business consequence / takeaway for a pentester?
- [ ] Does "how to use it in practice" include: trigger cues, minimal verification, judging the result, next step, impact proof?
- [ ] For 🔴 Web-vulnerability points, is there a "code-level" comparison (flawed code vs fixed code, marking source and sink)?
- [ ] Any fabricated CVE IDs, company names, or amounts? (Must be zero)

## D. Honesty and verifiability
- [ ] Is all content you added marked with "🔎 Added"?
- [ ] Are uncertain version numbers, figures, and parameters in the "pending verification" list rather than written down as fact?
- [ ] Are errors in the original notes pointed out and explained, rather than quietly corrected?
- [ ] Were all sources used for verification non-mainland-China sources?

## E. Structure and format
- [ ] Is the output a `.md` file delivered via `present_files` (when the user did not ask for another format)?
- [ ] Is it rated by the four tiers (🔴 Core / 🟡 Important / 🟢 Awareness / ⚪ Skim), at the **specific knowledge-point / subsection** level rather than one level for the whole note?
- [ ] Does every tier label carry half a line on "how to treat it" (e.g. "⚪ Skim — rarely encountered, just know the name")?
- [ ] Does the top info block have an "Overall rating for this note" line and the four-tier legend?
- [ ] Are 🟢 and ⚪ clearly distinguished: 🟢 has transferable thinking + reference pointers, ⚪ is only one or two lines with no steps or code?
- [ ] Does the rating combine the pentest / vuln-research direction and real-engagement frequency? Are niche, outdated, or specific-old-version items pushed down to ⚪?
- [ ] Does the depth match the tier (⚪ written as a long passage, or 🔴 as one line, both fail)?
- [ ] For concepts already covered in earlier notes, are they only referenced rather than repeated, and do the referenced notes actually exist?
- [ ] Is there a "methodology overview" and a "self-test"?
- [ ] Is the reply only a brief explanation, without pasting the whole set of notes again?

## F. Boundaries
- [ ] Is "authorized environments / labs / CTF only" written once at the top?
- [ ] Any attack plan against a specific real target, or complete ready-to-deploy malicious programs? (Must be zero)

---

## Common failure modes (symptom -> fix)

| Symptom | Fix |
| --- | --- |
| The notes are just the original text reformatted | Back to Step 3: add root cause and the three questions to every point |
| Long but without focus | Back to Step 2: re-rate, compress 🟢 into a paragraph and ⚪ into one or two lines |
| Reader can't tell what can be skipped | Check whether 🟢 / ⚪ are mixed up; re-judge by "will this thinking help me think of something later" |
| Whole note has only one level | Split to subsection granularity and label separately (principle, setup steps, harm extension are often at different levels) |
| Vague cases | Go to case-anchors.md for a real case, or rewrite as an example scenario with business nouns |
| The reader cannot tell what was added | Add the "🔎 Added" marker |
| Commands explained in usage but not in reason | Rewrite as "fragment / what it does / why it is needed" |
