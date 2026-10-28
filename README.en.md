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
5. **How to use it in practice** — when to think of it -> how to verify -> how to judge the result -> what to do next
6. **Defense and detection view** — knowing how the defender fixes it tells you where fixes leak
7. **Common mistakes** — frequent misconceptions and troubleshooting leads

Whenever a command, payload, or tool parameter appears, it is **broken down into every fragment**: what this fragment is,
what it does, why it is needed — plus what normal output looks like and how to read it.

### Relevance rating

Not every point gets the same depth. Relevance to real pentest work is judged first, and **the rating is written into the
notes**:

| Level | Criteria | Treatment |
| --- | --- | --- |
| 🔴 Core | Appears directly in the pentest workflow, or builds "vulnerability intuition" (SQL Injection, XSS, SSRF, file upload, reconnaissance, privilege escalation, lateral movement) | Full 7-module expansion, with a real case |
| 🟡 Supporting | Fundamentals that back the core skills (HTTP details, encoding, common middleware) | Keep "what / why / how", case may be brief |
| ⚪ Awareness | Only loosely related to real pentest work (compliance clauses, history of obscure protocols) | One short paragraph, plus why it is low priority |

### Honest labeling

- Anything **not in the source material that the assistant added** is marked with a standard callout:
  `> [!note] 🔎 Added (not in source notes)`, so you can verify it yourself.
- Version numbers, CVE IDs, figures, and parameters that are uncertain are **not written down from memory as fact**;
  anything unverifiable goes into a "pending verification" list.
- Where the original notes are plainly wrong, the error is pointed out with the correct approach, not silently fixed.
- **No CVE IDs, company names, or loss figures are ever fabricated.**

---

## Known caveat

In Step 7 of `SKILL.md`, the default output directory is written as `/mnt/user-data/outputs/`, a **Linux / container**
path that has no equivalent on Windows (it typically resolves somewhere under the application install directory, so the
generated files end up where you would never look).

Both language versions in this repository are kept faithful to the original and are **not modified**. If you use this on
Windows, change that line to a directory inside your workspace, for example:

```markdown
Save to the `outputs/` subdirectory of the current workspace; if there is no workspace, save to
`C:\Users\<your-username>\WorkBuddy\outputs\`.
```

---

## Boundaries and bottom lines

- Notes are meant for **learning and authorized security testing**. Content involving attack steps carries one reminder of "authorized environments / labs / CTF only".
- Payloads and commands used to explain principles stay at **course and lab teaching** granularity; no attack plans targeting a **specific real, unauthorized target**.
- No complete, directly deployable malicious programs (finished ransomware, AV-evading trojans). When a principle needs explaining, only the mechanism and detection ideas are covered.

---

## License

MIT
