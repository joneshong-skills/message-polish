---
name: message-polish
description: >-
  Polish draft messages for professional business communication. This skill should be used when the user asks to "潤稿", "幫我修改這段話", "polish this message", "修一下措辭", "這樣寫好嗎", "幫我潤一下", "tone check", "rewrite this", pastes a draft message for refinement, or discusses improving wording, tone, or professionalism of existing text (LINE messages, emails, client replies, quote annotations, business proposals).
version: 0.1.0
io:
  input:
    - mime: "text/plain"
      description: "Draft message to polish"
  output:
    - mime: "text/markdown"
      description: "Polished message"
---

# Message Polish

## Principles

**Polish**: Fix tone, clarity, logical flow, redundancy, and passive-aggressive undertones.
**Preserve**: Author's personality, intent, and key information. Retain warmth and humor where appropriate.
**Explain**: Every change with a brief reason (under 20 words).

## Tone Spectrum

| Register | Context | Language Marker | Constraint |
|----------|---------|-----------------|-----------|
| **Formal** | Contracts, legal, official notices | "Please proceed per the specified terms" | No colloquialisms, strict grammar |
| **Professional-warm** | Client messages, emails | "Let's get this done on schedule—happy to help" | Default. Balance professionalism with approachability |
| **Casual-professional** | Internal team, familiar collaborators | "Let's wrap this up by EOW" | Conversational, informal if unambiguous |

**How to select**: Determine register from recipient role (external = formal/warm, internal = casual). If ambiguous, default to Professional-warm.

## Chinese Business Pitfalls

| Avoid | Use Instead | Reason |
|-------|-------------|--------|
| 你應該… | (remove or soften) | Prescriptive |
| 麻煩你… | 能否協助… / 方便的話… | Less assumptive |
| 否則… | 亦可由… | More open-ended |
| 雙贏 | 互利合作 / 各取所長 | Avoids cliché |
| 幫助你的公司 | 幫到公司 | More direct |
| 確定這是你要的 | 確認方向對了 | Less assumptive |

## Workflow

### 1. Identify Context

Determine recipient, channel, and intent from the draft and request.
- **Default if not specified**: recipient = peer/stakeholder, channel = email, tone = professional-warm.
- **If user provides context**, use it. If output-only mode is requested, proceed directly to step 2.

### 2. Diagnose Priority Issues

**Procedure**:
1. Scan the draft for each issue type in the table below (top-to-bottom order = priority rank).
2. Count total types present.
3. **If ≤3 types**: Address all of them.
4. **If >3 types**: Address the first 3 in table order; then ask "Which of the remaining issues should I prioritize?"

| Issue | Example | Fix Rule |
|-------|---------|----------|
| Passive-aggressive | 「否則承辦方將自行購買」 | Reframe as neutral options |
| Presumptuous | 「你應該也比較放心」 | Remove assumptions about recipient's feelings |
| Cliché | 「雙贏」「共創價值」 | Replace with specific language |
| Run-on topics | 「下週啟動項目。順便說，最近看新劇不錯」 | Split with natural transition |
| Hedging overload | 「可能也許大概…」 | Commit to a stance |
| Redundancy | 「這個方案我們已經深入討論過，我們經過充分考慮」 | Keep the stronger version |
| Register mismatch | 「茲將通知尊敬的客戶，咱們現在趕快幹這事」 | Unify tone |

### 3. Output Format

**Polished version** in blockquote (copy-paste ready):

> [polished message]

**Change notes**: One line per change.
- Format: `[line X, phrase "xxx"] issue-type: original → polished (reason)`.
- Example: `[line 3, phrase "可能也許"] hedging-overload: 「可能也許」→ removed (commit to timeline)`.
- Each note: under 20 words.

### 4. Respond to Feedback

Accept refinements and re-output.

## Constraints

**Recipient Formality Map**: Explicit mapping for register selection when recipient type is specified:
- **Formal**: Legal stakeholders, government, senior external executives, compliance officers, first-time external contacts.
- **Professional-warm**: Clients, vendors, internal directors, colleagues across teams.
- **Casual-professional**: Direct reports, core team members, long-term collaborators with established rapport.

**Register Lock-in**: Once register is determined (step 1), hold it constant across all subsequent versions unless user explicitly requests a shift. Do not drift toward neighboring registers due to rewording efficiency.

**Tone Drift Tolerance**: Tone shifts must not exceed one level on the Tone Spectrum. Cannot change from Formal to Casual-professional in a single pass. If user feedback suggests a two-level shift is needed, ask for confirmation: "This would shift from [register A] to [register C]—is this intentional?"

**Do Not Polish If**: Decline and recommend another skill for:
- Translating to another language
- Creating new content (not refining existing draft)
- Legal or compliance review (out of scope; refer to legal skill)
- Applying external style guide (corporate branding guide, AP style, etc.)
- Messages where tone-shifting is the primary goal and content is secondary (use brainstorming skill instead)

**One-Question Rule**: Ask at most one clarifying question per exchange. Always provide a best-guess default.

**Output-Only Mode**: When the user explicitly requests output-only delivery using any of these phrases:
- 「直接給」「只輸出結果」「just output」「skip explanation」「output only」「don't explain」
→ Deliver the polished message immediately in blockquote format (Step 3).
→ Add one line of assumptions: `Assumed: recipient=[specific role or type], channel=[email/LINE/etc], register=[formal/professional-warm/casual-professional]`.
→ Skip all explanations and change notes.

**Priority Issues Limit**: Addressed in Workflow Step 2. If >3 issue types present, handle first 3 in table order and ask user to prioritize remaining issues explicitly.

**Iteration Protocol**: When user provides feedback on the same issue type in a **follow-up message** (second round of corrections for that type), ask for explicit direction: "Which aspect of [issue-type] should I focus on?" Do not re-polish that issue type without user guidance.

**Paraphrase Depth**: Preserve all main subjects and key commitments. Tone shifts must not exceed one level on the Tone Spectrum.
- Define "fundamental elements" as: (1) primary subject, (2) key commitment or promise, (3) stated intent.
- If changing >2 of these 3 elements, ask the user which to prioritize.

**Length**: Within ±15% of original word count.

**Content**: Rephrase only. No facts added, removed, or invented.

**Voice**: Preserve author's personality, phrases, idioms, and humor. Remove: filler words ("basically", "like"), hedging language ("maybe", "probably"), redundant apologies.

**Format Stability**: After initial blockquote delivery, maintain the same line breaks and paragraph structure in all subsequent versions.