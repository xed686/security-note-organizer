# security-note-organizer

A **Skill for AI assistants** (WorkBuddy / Claude and similar): turns cybersecurity class notes, video transcripts, lab
logs, and article material into **deep-learning notes written for security beginners**.

Its output is not "the same notes with nicer formatting", but a set of notes you can **understand on first read and
actually use in an authorized penetration test**.

**Languages**: this repository ships both a **Chinese version** (repository root) and an **English version** (`en/`).
See [README.md](./README.md) for the Chinese documentation.

---

## What it solves

Security learners usually hold fragmented material: it records *what to do*, drops *why*, and never connects to real
business impact. Studying from notes like that gets you through an exam, but is useless in practice.

So this Skill requires the notes it produces to do four things:

| Goal | Meaning |
| --- | --- |
| **Understandable** | Every concept has a plain-language explanation and an analogy, no term-stacking |
| **Thorough** | The principle, the reasoning, and the **purpose of every step** are written out |
| **Usable** | It answers "on a real target, when do I think of this, how do I verify it, what do I do next" |
| **Business-anchored** | Key points are tied to real cases or typical business scenarios, landing the knowledge on concrete systems and losses |

The writing perspective is: **a senior industry expert teaching a genuine beginner** (Feynman style) — assume the reader
has zero prior knowledge, but is smart and willing to listen carefully.

---

## Repository structure

```
security-note-organizer/
├── README.md                         # Chinese documentation (this repo's default)
├── README.en.md                      # English documentation (this file)
├── SKILL.md                          # Chinese skill: 7-step workflow + boundaries
├── references/                       # Chinese reference files
│   ├── note-template.md              # Note skeleton (build from this before drafting)
│   ├── teaching-method.md            # Writing explanations, analogies, step breakdowns
│   ├── case-anchors.md               # Real-case anchor library, indexed by vuln type
│   └── self-check.md                 # Pre-delivery self-check
├── en/                               # Full English skill, independently installable
│   ├── SKILL.md
│   └── references/
│       ├── note-template.md
│       ├── teaching-method.md
│       ├── case-anchors.md
│       └── self-check.md
└── security-note-organizer.skill     # Packaged original (zip, importable as-is)
```

Both the root (Chinese) and `en/` (English) folders are complete, independently installable skills.

---

## Installation

### Option 1: use the packaged file

Download `security-note-organizer.skill` and unzip it into your skills directory.

### Option 2: clone from this repository

Chinese version:

```bash
# User-level install (available to all projects)
git clone https://github.com/xed686/security-note-organizer.git \
  ~/.workbuddy/skills/security-note-organizer
```

English version:

```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/xed686/security-note-organizer.git \
  ~/.workbuddy/skills/security-note-organizer-en
cd ~/.workbuddy/skills/security-note-organizer-en && git sparse-checkout set en
```

> For project-level use, clone into `{project}/.workbuddy/skills/security-note-organizer/` instead.
> Note: the English skill declares `name: security-note-organizer-en`, so it can be installed alongside the Chinese one
> without a name collision.

---

## Usage

Once installed, just paste your material to the AI assistant — no need to invoke it by name. Typical triggers:

- "Organize my security notes"
- "Turn this lecture into notes"
- "Explain this vulnerability and write it up"

Even if you only paste material and never say "organize", the workflow kicks in automatically as long as the content is
about penetration testing, web security, reconnaissance, internal networks, privilege escalation, vulnerability
principles, tooling, or Android reversing.

### Supported input types

Class notes / video transcript / lab log / article or document / screenshot / just a few keywords.

When the input is fragmented or very short, it will **not** fire back a pile of questions — it makes a reasonable
inference and proceeds, marking inferred parts explicitly. It asks a single clarifying question **only when the topic is
completely undeterminable**.

---

## What the notes look like

Every knowledge point expands along the "skeleton for real understanding" (the core idea: **every step has a why**):

1. **What it is** — a one-sentence definition plus an everyday-life analogy
2. **Why it exists** — the root cause behind the vulnerability or technique (beginners lack this most, and it is the source of vulnerability intuition)
3. **How to do it** — step by step, each step answering: what you do, **why you do it**, what you get
4. **What it looks like in a business** — a real case / typical business scenario
5. **How to use it in practice** — when to think of it -> how to verify -> how to judge the result -> what to do next ->
   **how to prove impact** (use minimal, non-destructive evidence of harm — it decides the vulnerability's rating)
6. **Defense and detection view** — knowing how the defender fixes it tells you where fixes leak
7. **Common mistakes** — frequent misconceptions and troubleshooting leads

Whenever a command, payload, or tool parameter appears, it is **broken down into every fragment**: what this fragment is,
what it does, why it is needed — plus what normal output looks like and how to read it. Core payloads also carry two
more lines: **environment prerequisites** (language version, extensions, config switches, directory permissions) and
**the most common reason it fails** — beginners rarely get stuck on "I did not know this trick existed", they get stuck
on "I copied it and it did not run".

### Four-tier rating

Not every point gets the same depth. Points are rated into four tiers first, then depth follows; **the rating is written
into the notes**:

| Tier | Meaning | Treatment |
| --- | --- | --- |
| 🔴 Core | High-frequency, general-purpose, transferable — the bread and butter | Full 7-module expansion, with a real case; Web-vuln points get a code-level comparison |
| 🟡 Important | Used in real engagements, but not every day | Write what / why / how / how-to-use clearly; state "where to look it up when needed" |
| 🟢 Awareness | Good to know it exists; the thinking can transfer | A short paragraph of concept + one line of transferable thinking; details for reference |
| ⚪ Skim | Rarely encountered / niche / outdated | One or two lines, just know the name; no steps, no code |

Rate at the **specific knowledge-point / subsection** level, not one level for the whole note; every tier label carries
half a line on "how to treat it".

### Three note types

The full skeleton (code comparison, real security incidents, "how to use it in practice") is designed for
**vulnerability notes**. The other two types swap parts instead of forcing the skeleton:

| Element | Vulnerability | Tooling and architecture | Methodology |
| --- | --- | --- | --- |
| "Case" | Real security incident | **Product case** (after checking README / official docs) or a labeled example scenario | Typical business scenario + example scenario |
| Principle | root cause + source/sink code comparison | Layering / structure diagram (who calls whom) + design trade-offs | Decision criteria (which signal points to which route) |
| "How to use it in practice" | Trigger cue -> minimal verification -> impact proof | **Selection judgment**: which task to use it for, which not | Decision branches |

### Honest labeling

- Anything **not in the source material that the assistant added** is marked with a standard callout:
  `> [!note] 🔎 Added (not in source notes)`, so you can verify it yourself.
- Version numbers, CVE IDs, figures, and parameters that are uncertain are **not written down from memory as fact**;
  anything unverifiable goes into a "pending verification" list.
- Where the original notes are plainly wrong, the error is pointed out with the correct approach, not silently fixed.
- **No CVE IDs, company names, or loss figures are ever fabricated.**

---

## Save and index (since v1.1)

Step 7 of `SKILL.md` is split into **7a save and index** and **7b self-check and delivery**. The note is no longer just
"written to a .md file" — it lands where the host environment's conventions say, and gets indexed so it can be found:

1. Put it in an **existing** category folder (create one only if nothing fits, and tell you).
2. Continue the folder's `00_`, `01_` numbering with the same family naming.
3. Add a line to the folder MOC's note list and insert the note into the relevant topic-thread chain.
4. Write real previous/next and related links in the new note; backfill a link in the **1–3 most related older notes**.
5. Platform differences: Obsidian gets `[[wikilinks]]`, a plain folder gets relative links; the body no longer hardcodes
   claude.ai's `/mnt/user-data/outputs/`.

If you really do use claude.ai, set the 7b save location to `/mnt/user-data/outputs/` and deliver with `present_files` —
that is now an option, not the default assumption.

---

## Boundaries and bottom lines

- Notes are meant for **learning and authorized security testing**. Content involving attack steps carries one reminder of "authorized environments / labs / CTF only".
- Payloads and commands used to explain principles stay at **course and lab teaching** granularity; no attack plans targeting a **specific real, unauthorized target**.
- No complete, directly deployable malicious programs (finished ransomware, AV-evading trojans). When a principle needs explaining, only the mechanism and detection ideas are covered.

---

## Changelog

**v1.2.0**

- **New "opening rules"** (Step 3): the first section must be "definition + everyday analogy + what damage it causes";
  syntax tables, glossaries and background comparisons go after "what it is / why it exists". The reader's order is not
  the author's order of knowledge.
- **New "analogy requirements"** (Step 3): at least one analogy per 🔴 / 🟡 subsection; where the mechanism is easy to
  misread, add a line on where the analogy breaks down; never explain one mechanism with two different analogies.
- **Step 2 gains an orientation rule**: 2–3 sentences before the map — what the note covers, where it sits in the
  workflow, what the reader can do afterwards.
- **Verification sources refined**: technique and diagnostic experience should come from a first-hand writeup (the
  researcher's own account, the vendor's incident report); second-hand tutorials are leads only.
- **Case-selection criterion** (case-anchors): prefer a case that teaches a judgment (severity rated, misjudgment
  corrected, chain escalated) over the most technically elaborate one; add "what judgment this case teaches".
- **teaching-method** gains a library of nine proven analogy skeletons plus density/no-piling rules; **self-check**
  gains two items (opening, analogy coverage).

**v1.1.0**

- **Step 7 split into "7a save and index" / "7b self-check and delivery"**: owning folder, `0X_` numbering, MOC entry
  and topic thread, backlinks to older notes, platform differences; claude.ai-only paths removed from the body
  (`present_files`, `/mnt/user-data/outputs/`).
- **New "three note types"**: vulnerability / tooling-and-architecture / methodology, with per-element substitution rules.
- **Verification is now three tiers**: **empirical test > web verification (non-mainland-China sources) > pending
  verification**; tests must state environment, command, and actual output, and Sources gets a separate "Verified by
  testing" line; conflicts with the source must be stated plainly.
- **New length criteria (no line counts)**: guard against grade inflation (🔴 on a minority of subsections, roughly
  ≤ 1/3) and duplication; five-line recap test; split into parts rather than compressing.
- **Core payloads / commands must state environment prerequisites + the most common failure cause.**
- **Self-check** gains: link validity (grep), index and backlinks, empirical items, length criteria. **Case library**
  gains file upload / LFI-to-RCE / path traversal skeletons plus "how to swap cases for non-vulnerability knowledge".
- Trigger description tightened; frontmatter gains `version / license / platforms / metadata`.
- Synced with the Chinese edition (v1.1.0), which this release mirrors.

---

## License

MIT
