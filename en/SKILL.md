---
name: security-note-organizer-en
description: >-
  Turn cybersecurity class notes, video transcripts, lab logs, and article material into deep-learning notes written for
  security beginners (Markdown by default). Notes are organized from the perspective of penetration testing and
  vulnerability research, following "what it is -> why it exists (root cause) -> how to do it (procedure and the purpose
  of every step) -> what it looks like in a real business (real cases) -> how to use it in practice", and anchoring key
  points to real-world cases or business scenarios so the knowledge does not stay superficial. Use this skill whenever the
  user says "organize my security notes", "turn this lecture into notes", "explain this vulnerability and write it up",
  or pastes notes or material about penetration testing, web security, reconnaissance, internal networks, privilege
  escalation, vulnerability principles, tooling, or Android reversing and wants it organized, completed, or explained —
  even if the word "organize" never appears.
---

# Cybersecurity Note Organizer

## What this skill solves

The reader is a **complete beginner in cybersecurity**, aiming at **penetration testing / vulnerability research**. The raw
material they hold (class notes, transcripts, articles) is usually fragmented: it records *what to do*, drops *why*, and
never connects to real business impact. Studying from notes like that gets you through an exam, but is useless in
practice.

So the output of this skill is not "the same notes with nicer formatting", but a set of study notes you can **understand
on first read and actually use in an authorized penetration test**:

- **Understandable**: every concept has a plain-language explanation and an analogy, no term-stacking.
- **Thorough**: the **principle, the reasoning, and the purpose of every step** are written out.
- **Usable**: it answers "on a real target, when do I think of this, how do I verify it, what do I do next".
- **Business-anchored**: key points are tied to **real cases or typical business scenarios**, so knowledge lands on
  concrete systems and concrete losses.

Write as **a senior industry expert teaching a genuine beginner** (Feynman style): assume the reader has zero prior
knowledge, but is smart and willing to listen carefully.

## Workflow

Follow the steps in order; do not skip. Details for each step live in `references` — read them when needed.

### Step 1: Figure out the input

Decide what the user provided: class notes / video transcript / lab log / article or document / screenshot / just a few
keywords.

- When the input is fragmented or very short, do **not** fire back a pile of questions. Make a reasonable inference and
  proceed, marking inferred parts per Step 4.
- Screenshots / PPT images: first recognize the text, commands, and diagrams in them; anything you cannot read clearly
  goes into "Pending verification" — do not guess.
- Ask a single clarifying question **only when the topic is completely undeterminable**.
- When the input is long and covers multiple topics, split it by knowledge point. If it is too large, produce it in
  batches and tell the user the split plan first.
- If the user mentioned earlier notes in the conversation (document name, course name), write it down — Step 6 uses it
  for cross-referencing. **Only reference notes that actually exist and that the user actually mentioned. Never invent
  links.**

### Step 2: Four-tier rating — how much effort the reader should spend

The point of rating is to let the reader **see at a glance how much effort each part deserves**: which to drill repeatedly,
which to just know how to look up, which to read once and archive, and which to skip outright. The rating also decides how
deep you write.

#### The four tiers

| Tier | Meaning | How the reader should treat it | How deep you should write |
| --- | --- | --- | --- |
| 🔴 Core | High-frequency, general-purpose, transferable — the bread and butter | Must truly understand + be able to reproduce; drill repeatedly | Full skeleton, all modules, with a real case; Web-vuln points include a code-level comparison |
| 🟡 Important | Used in real engagements, but not every day | Understand the principle; know how to look it up and use it — no need to memorize | Write clearly what / why / how / how-to-use; state "where to look it up when needed" (tool docs, cheat sheet, parameter tables) |
| 🟢 Awareness | Good to know it exists; the thinking can transfer | Read once to build the concept; no need to master; keep for reference | A short paragraph stating the concept + one line on the transferable thinking; compress details or give lookup pointers only — no full steps |
| ⚪ Skim | Rarely encountered / niche / outdated | Glance once; just know the name; don't spend time | One or two lines: name + one-line what-it-is + why skim (e.g. "depends on an old version, rarely seen in the wild"). No steps, no code |

#### The 🟢 vs ⚪ distinction must be made clear (the core value of this rating)

These two tiers are the easiest to confuse, and the judgment the reader needs most: **which can be skipped entirely**.

- 🟢 Awareness: **the concept is worth knowing, details are for reference**. Its thinking can transfer to other scenarios, so read it once and form an impression; just don't memorize the details — look them up when needed.
- ⚪ Skim: **don't even read the details — just knowing it exists is enough**. It is barely encountered, or its thinking has little transfer value; spending time on the details is wasted.

Rule of thumb: **"Later, when I run into something else, will this thinking help me think of something?"** Yes → 🟢; no, just knowing the name → ⚪.

#### Rate at the knowledge-point granularity, not one level per whole note

Within a single note, even within a single section, different parts can be at completely different levels — they must be
**labeled separately**. For example, a lesson on a vulnerability environment:

- The core understanding of the vulnerability (why this hole exists) → 🟡
- The environment-setup steps / demo code → ⚪
- The harm-extension thinking (what it can combine with) → 🟢

Another example: for a historical vulnerability tied to a specific old version, the **vulnerability itself** may be ⚪, but
the **principle** it embodies (e.g. "input is executed as code") may be 🔴. Label the principle and the specific
vulnerability separately; explain the principle thoroughly as usual.

#### How to decide the level

Combine two dimensions: **the user's career direction (pentest / vulnerability research)** and **how often it is used in
real engagements**.

- Move up: high-frequency, general-purpose, recurring in the pentest workflow, thinking that transfers a lot (e.g. SQL
  Injection, reconnaissance, privilege escalation's general thinking).
- Push down to ⚪: niche techniques you might never meet, outdated techniques, vulnerabilities that only work on a specific
  old version, discontinued protocols or products.
- When unsure, ask yourself: "Roughly how many times a year would a pentester use this?" Often → 🔴; on projects → 🟡;
  occasionally as a thinking cue → 🟢; basically never → ⚪.

#### How to present it in the notes

1. Add a line "**Overall rating for this note**" to the info block at the top — one sentence telling the reader whether the
   note as a whole should be read closely or skimmed, and point out the few things that must be remembered. Example:
   "Overall this note is mainly 🟢 / ⚪ — skim to build concepts and keep for reference; just remember points XX and YY."
   Also attach the four-tier legend.
2. After **each section / subsection heading**, label the tier, and add half a line on "how to treat it" so the reader does
   not have to go back to the legend. Examples:
   - `🔴 Core — must master, reproduce hands-on`
   - `🟡 Important — understand the principle, look it up when used`
   - `🟢 Awareness — read once, keep for reference`
   - `⚪ Skim — rarely encountered, just know the name`

   The half-line can be reworded to fit (e.g. "🟢 Awareness — just look it up on the way"), but always say clearly "how to
   treat it".
3. In the "map" table at the top of the note, list the level of each knowledge point, so the reader sees the big picture
   before deciding the close-reading order.

### Step 3: Expand each knowledge point in depth

For 🔴 / 🟡 points, organize with the "skeleton for real understanding" below; for 🟢 / ⚪, follow the length guidance in
the Step 2 table and do not apply the full skeleton. The full template is in `references/note-template.md`; writing
technique is in `references/teaching-method.md`.

Skeleton for real understanding (the core idea: **every step has a why**):

1. **What it is**: a one-sentence definition plus a everyday-life analogy.
2. **Why it exists (principle / root cause)**: the fundamental reason behind the vulnerability or technique. Beginners
   lack this most, and it is the source of vulnerability intuition. For 🔴 Web-vulnerability points, also add a
   short segment on **what it looks like at the code level**: a flawed illustrative snippet versus the fixed one, marking
   source (where user input enters) and sink (where the dangerous function is). Black-box testing teaches "how to try";
   the code level teaches "why exactly here" — the source of vulnerability-research and code-audit intuition. Keep the
   code minimal and illustrative.
3. **How to do it (procedure)**: step by step, each step answering three fixed things: what you do, **why you do it**,
   and what you get (plus what it means if it fails).
4. **What it looks like in a business**: a real case / typical business scenario, per Step 5.
5. **How to use it in practice**: when to think of it -> how to verify -> how to judge the result -> what to do next ->
   **how to prove impact**. The last item means: use minimal, non-destructive evidence to show what harm this bug can
   actually cause (what data can be read, what can be controlled). In Bug Bounty and pentest reports, vulnerabilities
   whose impact is unclear are often downgraded or rejected, so this item matters as much as "finding the vulnerability".
6. **Defense and detection view**: brief. Knowing how the defender fixes it tells you where fixes leak and where bypass
   ideas come from.
7. **Common mistakes**: beginner misconceptions and troubleshooting leads.

Whenever a command, payload, or tool parameter appears, **break it down into every fragment**: what this fragment is, what
it does, why it is needed — plus what normal output looks like and how to read it.

### Step 4: Fill the gaps and label honestly

Source notes usually have holes. Filling them is the value of this skill — but the reader must be able to tell **which
parts are their original notes and which parts you added**, otherwise nothing can be verified.

- Anything **not in the source material that you added** (principles, cases, background) uses one standard callout block:
  `> [!note] 🔎 Added (not in source notes)`
- Details you are unsure about (version numbers, CVE IDs, specific figures, tool parameters) must **not be written down
  from memory as fact**. If you have web search, verify them, and verify **only against non-mainland-China sources**
  (English-language authoritative sites, vendor advisories, NVD, major security vendors' English blogs). If you cannot
  verify, write "roughly / needs verification" and put it in the "Pending verification" list at the end of the notes.
- Where the original notes are plainly wrong, point it out and give the correct approach. Do not silently fix it.

### Step 5: Anchor the knowledge to real business (case anchors)

This is what the user values most. Every key point gets at least one case, so the reader sees **how this flaw actually
went wrong inside a real company**.

- Prefer **real, publicly verifiable incidents** (vulnerabilities with CVEs, publicly disclosed data breaches). Commonly
  used cases are collected in `references/case-anchors.md`, indexed by vulnerability type.
- Every case is told in four fixed beats: **what happened -> which link was the root cause (matching which point in these
  notes) -> what business consequence it caused -> what a pentester learns from it**.
- When no suitable real case exists, substitute a **typical business scenario** (e.g. "e-commerce order lookup API") and
  clearly label it "Example scenario". Never present fictional content as a real incident.
- **Never fabricate CVE IDs, company names, or loss figures.** If unsure, describe only the nature of the incident, no
  numbers.

### Step 6: Cross-references and terminology

- If a concept used here was **already explained in the user's earlier notes**, do not expand it again — write "see
  *Notes on X*" and recap it in one sentence.
- Always use the **standard industry English term** (Web Shell, Payload, Reverse Shell, Privilege Escalation). **Do not
  force-translate them.** Explain the meaning in the local language the first time they appear.
- Write in English, in the voice of a patient teacher.

### Step 7: Finalize and self-check

- Default output is a **Markdown file** (`.md`). In claude.ai, save it to `/mnt/user-data/outputs/` and deliver with
  `present_files`; in other environments such as Claude Code, save to the current working directory or a user-specified
  location (e.g. the user's notes library). If the user explicitly asks for another format (Word, PDF, etc.), follow
  that and read the corresponding format skill first.
- Filename: a concise title, e.g. `sql-injection-union-based-notes.md`.
- Before delivery, check the draft item by item against `references/self-check.md`. Fix anything that fails, then deliver.
- Keep the reply short: what ratings you applied, what you added, what needs verification. **Do not paste the whole set of
  notes back into the reply.**

## Boundaries and bottom lines

- Notes are meant for **learning and authorized security testing**. For content involving attack steps, one reminder of
  "authorized environments / labs / CTF only" at the start is enough — do not repeat it in every section.
- Payloads and commands used to explain principles stay at **course and lab teaching** granularity. Do not generate
  attack plans targeting a **specific real, unauthorized target**.
- Do not write complete, directly deployable malicious programs (finished ransomware, AV-evading trojans). When the
  principle needs explaining, explain the mechanism and detection ideas.

## File index

| File | When to read it |
| --- | --- |
| `references/note-template.md` | Before drafting, to build the skeleton |
| `references/teaching-method.md` | When writing explanations, analogies, step breakdowns |
| `references/case-anchors.md` | In Step 5, when you need a real case |
| `references/self-check.md` | Before delivery, for the self-check |
