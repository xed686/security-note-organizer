# Note Output Template

Build the skeleton from this template when drafting. Brackets【】mark content you need to fill in. Length follows the
four-tier rating (rules in SKILL.md Step 2): 🔴 Core uses the full 7 modules; 🟡 Important keeps modules 1, 2, 3 and 5 and
states where to look it up when needed; 🟢 Awareness is a short paragraph of concept + transferable thinking; ⚪ Skim is
one or two lines.

Rate at the **specific knowledge-point / subsection** level, not one level for the whole note; every label is followed by
half a line on "how to treat it".

---

## Overall skeleton

````markdown
# 【Note title】

> [!info] 🧭 Knowledge map
> Belongs to:【user's knowledge-base home page, if they mentioned one】 ｜ Previous:【a note that really exists, otherwise "TBD"】 ｜ Next:【same】
> 🔗 Related:【only notes the user actually mentioned and that really exist】

> One-line summary:【the single most important takeaway — a beginner who reads this line knows what they learned】
> Source:【course / article / lab name; parts added by Claude are marked with "🔎 Added"】
> Preconditions: authorized environments, labs, and CTF only.
> **Overall rating for this note**:【one sentence telling the reader whether the whole note should be read closely or
  skimmed, and point out the few things that must be remembered. Example: "Overall this note is mainly 🟢 / ⚪ — skim to
  build concepts and keep for reference; just remember points XX and YY."】

> [!tip] 📊 Rating legend
> 🔴 Core — high-frequency, general-purpose bread and butter: must truly understand + reproduce, drill repeatedly
> 🟡 Important — used in real engagements but not every day: understand the principle, look it up and use it, no need to memorize
> 🟢 Awareness — concept worth knowing, details for reference: read once to build the concept, keep for reference
> ⚪ Skim — rarely encountered / niche / outdated: just know the name, no need to spend time

---

## 0. Start with this map

【What this piece covers, where it sits in the penetration testing workflow, what you can do after learning it】

| Knowledge point | Tier | Position in the pentest workflow | One-line purpose |
| --- | --- | --- | --- |
| 【Point A】 | 🔴 Core | 【e.g. vulnerability discovery / exploitation / reconnaissance】 | 【one line】 |
| 【Point B】 | 🟡 Important | 【】 | 【】 |
| 【Point C】 | 🟢 Awareness | 【】 | 【】 |
| 【Point D】 | ⚪ Skim | 【】 | 【】 |

**Suggested reading order**:【which parts to read closely first, which can be skipped】

**Prerequisites**:【what you need to know first. If earlier notes covered it, write "see *Notes on X*" and recap it in one sentence】

---

## 1. 【Point A】🔴 Core — must master, reproduce hands-on

### 1.1 What it is
【One-sentence definition】
> Analogy:【an everyday-life metaphor that helps a first-time reader build a mental picture】

### 1.2 Why it exists (principle)
【Root cause. Make clear "what assumption the programmer / designer made, and where, that caused the problem here"】

【If there is a data flow, draw it with text arrows or mermaid: user input -> program processing -> dangerous function / operation -> result】

**What it looks like at the code level** (applies to Web-vulnerability types; can be omitted for others)

```【language】
// ❌ Flawed version: mark source (where input comes from) and sink (where the dangerous operation is)
【minimal illustrative code】
```

```【language】
// ✅ Fixed version
【minimal illustrative code】
```

【One or two sentences: why the fix works; what kind of code should raise an alarm during code audit】

### 1.3 How to do it (procedure)

**Step 1:【action name】**
- What to do:【concrete operation】
- Why do it:【the purpose of this step — what it rules out / what it verifies】
- What you get:【expected observation】
- If it is not the expected result:【what that means, and how to adjust next】

**Step 2: ...**(same four items)

Command / payload breakdown:

| Fragment | What it does | Why it is needed |
| --- | --- | --- |
| 【fragment】 | 【】 | 【】 |

What normal output looks like and how to read it:【】

### 1.4 What it looks like in a business (case anchor)
【See case-anchors.md. Four fixed beats: what happened -> root cause matching which link in these notes -> business consequence -> takeaway for a pentester】

### 1.5 How to use it in practice
- **When to think of it**:【trigger cues, e.g. "a parameter is concatenated straight into a query", "the URL is supplied by the user"】
- **How to verify**:【the cheapest way to confirm, and how to avoid damaging the target】
- **How to judge the result**:【which observation counts as confirmed, which counts as not confirmed】
- **Next step**:【what to do once confirmed; the alternative line of thinking if not confirmed】
- **How to prove impact**:【use minimal, non-destructive evidence to show the harm: what data can be read, what can be
  controlled, how many users are affected. In a report this decides whether the vulnerability is accepted and how it is rated】

### 1.6 Defense and detection view
【How developers usually fix it; why the fix is sometimes incomplete. Keep it brief】

### 1.7 Common mistakes
- 【Beginner misconception 1: what is wrong, what the correct understanding is】
- 【Troubleshooting leads】

---

## 2. 【Point B】🟡 Important — understand the principle, look it up when used
(Keep 1.1, 1.2, 1.3, 1.5; the case can be one or two sentences)

**Where to look it up when needed**:【tool official docs, cheat sheet, parameter tables, etc.; no need to memorize】

## 3. 【Point C】🟢 Awareness — read once, keep for reference
【A short paragraph stating the concept】

**Transferable thinking**:【one line: in what future scenario this thinking helps you think of something】
**Details for reference**:【where the details can be looked up; no full steps】

## 4. 【Point D】⚪ Skim — rarely encountered, just know the name
【One or two lines: name + one-line what-it-is + why skim (e.g. depends on an old version, rarely seen in the wild / discontinued)】

---

### Example of mixed-tier grading within one section

When different parts of a section are at different levels, label them at the subsection level, not one level for the whole
section:

```markdown
## N. 【Some vulnerability-environment lesson】

### N.1 Why this vulnerability exists 🟡 Important — understand the principle, look it up when used
【principle explanation】

### N.2 Environment setup steps and demo code ⚪ Skim — lab-specific, just know this step exists
【one or two lines, no detailed steps】

### N.3 Harm extension: what it can combine with 🟢 Awareness — read on the way, build the thinking
【a short paragraph + transferable thinking】
```

---

## 5. Putting it together: methodology overview
【String this piece's methods into one decision flow, e.g. "spot something suspicious -> verify -> confirm the type -> exploit -> assess impact". Use mermaid or an arrowed text flow, and mark the decision basis at every branch】

## 6. Self-test (think it through before opening the answers)
1. 【In your own words: why does a certain principle hold】
2. 【Scenario question: given a business scenario, how would you start】
3. 【Troubleshooting question: when the observation is not as expected, what could be the causes】

<details>
<summary>Suggested answers</summary>

【Answer outline】

</details>

## 7. Pending verification / doubts
- 【Content you are unsure about, needing user or official-source verification】
- 【Suspected errors in the original notes, with explanation】

## 8. Sources
- 【Original notes / course】
- 【Material consulted for the added content (non-mainland-China sources)】
````

---

## How to write the added-content callout

```markdown
> [!note] 🔎 Added (not in source notes)
> 【The principle / case / background you added. State clearly that this part does not come from the source material】
```

## Other formats

Default is `.md`. If the user asks for Word / PDF, keep the same skeleton and only change the presentation, and read the
corresponding format skill first.
