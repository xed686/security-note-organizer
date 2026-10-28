# Note Output Template

Build the skeleton from this template when drafting. Brackets【】mark content you need to fill in. 🔴 Core knowledge
points use the full 7 modules; 🟡 Supporting points keep modules 1, 2, 3 and 5, with an optional brief case; ⚪ Awareness
points get a short paragraph only.

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

---

## 0. Start with this map

【What this piece covers, where it sits in the penetration testing workflow, what you can do after learning it】

| Knowledge point | Relevance | Position in the pentest workflow | One-line purpose |
| --- | --- | --- | --- |
| 【Point A】 | 🔴 Core | 【e.g. vulnerability discovery / exploitation / reconnaissance】 | 【one line】 |
| 【Point B】 | 🟡 Supporting | 【】 | 【】 |

**Prerequisites**:【what you need to know first. If earlier notes covered it, write "see *Notes on X*" and recap it in one sentence】

---

## 1. 【Point A】(🔴 Core)

### 1.1 What it is
【One-sentence definition】
> Analogy:【an everyday-life metaphor that helps a first-time reader build a mental picture】

### 1.2 Why it exists (principle)
【Root cause. Make clear "what assumption the programmer / designer made, and where, that caused the problem here"】

【If there is a data flow, draw it with text arrows or mermaid: user input -> program processing -> dangerous function / operation -> result】

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

### 1.6 Defense and detection view
【How developers usually fix it; why the fix is sometimes incomplete. Keep it brief】

### 1.7 Common mistakes
- 【Beginner misconception 1: what is wrong, what the correct understanding is】
- 【Troubleshooting leads】

---

## 2. 【Point B】(🟡 Supporting)
(Keep 1.1, 1.2, 1.3, 1.5; the case can be one or two sentences)

## 3. 【Point C】(⚪ Awareness)
【A short paragraph + one sentence on why it is low priority for pentesting】

---

## 4. Putting it together: methodology overview
【String this piece's methods into one decision flow, e.g. "spot something suspicious -> verify -> confirm the type -> exploit -> assess impact". Use mermaid or an arrowed text flow, and mark the decision basis at every branch】

## 5. Self-test (think it through before opening the answers)
1. 【In your own words: why does a certain principle hold】
2. 【Scenario question: given a business scenario, how would you start】
3. 【Troubleshooting question: when the observation is not as expected, what could be the causes】

<details>
<summary>Suggested answers</summary>

【Answer outline】

</details>

## 6. Pending verification / doubts
- 【Content you are unsure about, needing user or official-source verification】
- 【Suspected errors in the original notes, with explanation】

## 7. Sources
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
