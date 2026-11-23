---
name: security-note-organizer-en
description: >-
  Turn cybersecurity class notes, transcripts, lab logs, and articles into deep-learning notes for security beginners
  (Markdown by default), following "what it is -> why it exists -> how to do it (purpose of every step) -> what it looks
  like in business -> how to use it in practice", anchoring key points to real cases or business scenarios.
  Use it when the user says "organize my security notes", "turn this lecture into notes", "explain this vulnerability
  and write it up", or pastes notes about pentesting, web security, recon, internal networks, privilege escalation,
  vulnerability principles, tooling, or reversing and wants them organized, completed, or explained — even if the word
  "organize" never appears.
version: 1.1.0
author: "xed686 (original) | local revision: Hermes Agent"
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [security, note-organizing, security-learning, teaching, obsidian]
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

#### Length: control it with grade inflation and duplication, not line counts

There is no absolute length cap — a genuinely large topic (say "file inclusion", covering the principle, four
exploitation routes, a whole family of wrappers, and a full lab walkthrough) *should* be long; forcing a line count only
makes you cut real content. Guard against two things instead:

1. **Grade inflation**: too many 🔴 labels means no priority at all. Healthy is 🔴 on a minority of subsections (roughly
   ≤ 1/3). If "environment setup" and "parameter tables" are marked 🔴, the rating was not a judgment.
2. **Duplication**: the same information written twice — stated in prose and copied again into a table, a full breakdown
   table for every payload, the "authorized environments only" reminder in every section. This is the main source of bloat.

Two signals that a note is too long:

- Can you recap the skeleton in **five lines or fewer**? If not, the structure is loose — the content is not too little.
- Could half the subsections be skipped without losing the main line? If so, those should be **downgraded**, not deleted.

When a topic genuinely does not fit, **split it into parts** (e.g. `00_` / `01_` siblings in the same family) instead of
compressing: split notes are each readable, compressed ones please nobody.

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

For 🔴 core payloads, commands, or configuration tricks, add two more lines: **environment prerequisites** (language
version, extensions, ini/system switches, directory permissions, whether login is required) and **the most common reason
it fails** (filtered, wrong path, unsupported version, no write permission). Beginners rarely get stuck on "I did not
know this trick existed"; they get stuck on "I copied it and it did not run".

### Step 4: Fill the gaps and label honestly

Source notes usually have holes. Filling them is the value of this skill — but the reader must be able to tell **which
parts are their original notes and which parts you added**, otherwise nothing can be verified.

- Anything **not in the source material that you added** (principles, cases, background) uses one standard callout block:
  `> [!note] 🔎 Added (not in source notes)`
- Details you are unsure about (version numbers, CVE IDs, specific figures, tool parameters) must **not be written down
  from memory as fact**. Work through three levels of confidence, strongest first:
  1. **Empirical test**: anything you can run locally, in a lab, or in an authorized environment — just run it. Payload
     semantics, filter behavior, ini switches, error wording: **one run beats ten articles**. Record the environment
     (language and version, OS), the command, and the actual output, and add a separate "Verified by testing" line under
     Sources.
  2. **Web verification**: for what you cannot test, use **only non-mainland-China sources** (English-language
     authoritative sites, vendor advisories, NVD, official docs, major security vendors' English blogs).
  3. **Pending verification**: if neither is possible, write "roughly / needs verification" and put it in the "Pending
     verification" list at the end — do not blur it with vague wording.
- When the source notes conflict with your test or verification result, **say so plainly** ("this payload fails in my
  environment; the correct form is ...") — neither silently correcting it, nor dropping your own test result to spare the
  original text.

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

### Step 7: Save, index, then self-check

**7a Save and index (settle "where, what name, and how it gets found" first)**

Inspect the host environment's existing conventions first; do not invent directories:

1. **Find the owning folder**: look at the user's knowledge-base structure and put the note into an **existing**
   category folder; create one only if nothing fits, and tell the user.
2. **Continue the numbering**: when the folder already uses `00_`, `01_` prefixes, **carry on** with the same family
   naming (e.g. `01_file-inclusion-principles-and-exploitation.md`); do not start a second style.
3. **Update the index**: add a line to the folder's MOC note list (with a folder tag) and insert the new note into the
   relevant "topic thread" chain.
4. **Backfill links**: write the real previous/next and related notes in the new note's navigation block; also add a
   backlink (`[[new-note-name]]`) in the **1–3 most closely related older notes**.
5. **Platform differences**: Obsidian gets `[[wikilinks]]`, a plain folder gets relative Markdown links; never hardcode
   one platform's private path (e.g. claude.ai's `/mnt/user-data/outputs/`).

**7b Self-check and delivery**

- Default output is a **Markdown file** (`.md`), placed per 7a. If the user explicitly asks for another format (Word,
  PDF, etc.), follow that and read the corresponding format skill first.
- Filename: a concise title plus the folder's numeric prefix, e.g. `01_file-inclusion-principles-and-exploitation.md`.
- Before delivery, check the draft item by item against `references/self-check.md`; fix anything that fails. **Verify
  "link validity" with a command** (grep every `[[link]]` against the existing filenames) instead of trusting memory.
- Keep the reply short: the ratings applied, what you added, where the note landed and which index entries changed, and
  what still needs verification or where a test result contradicts the source. **Do not paste the whole note back.**

## Three note types: same steps, different parts

The full skeleton (source/sink code comparison, real security incidents, "how to use it in practice") is designed for
**vulnerability notes**. When the material is one of the other two types, swap the parts below — do not force the
skeleton, and do not use the swap as an excuse to skip the why.

| Element | Vulnerability | Tooling and architecture (agents, frameworks, platforms) | Methodology (process, reasoning, criteria) |
| --- | --- | --- | --- |
| Rating basis | CTF / bug-bounty frequency, can it be reproduced | Will it be obsolete in six months; **transferable models before specific product names** | How often it is used; does it directly drive the next action |
| Principle | root cause + source/sink code comparison | Layering / structure diagram (who calls whom) + design trade-offs | Decision criteria (which signal points to which route) |
| "Case" | Real security incident (see `case-anchors.md`) | **Product case** (1–2 real projects, after checking README / official docs) or a labeled example scenario | Typical business scenario + labeled example scenario |
| "How to use it in practice" | Trigger cue -> minimal verification -> impact proof | **Selection judgment**: which task to use it for, which not, the cost of choosing wrong | Decision branches: in which situation, take which route |
| Common failure | Memorizing payloads without the why | Listing features; presenting fast-decaying details as the point | Slogans with no criteria |

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
| `references/case-anchors.md` | In Step 5, when you need a real case (includes file upload / file inclusion; also how to swap cases for non-vulnerability knowledge) |
| `references/self-check.md` | Before delivery, for the self-check |
