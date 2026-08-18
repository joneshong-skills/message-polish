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

**How to select**: If recipient role is external (legal stakeholders, government, senior executives, first-time contacts) → Formal. If external but ongoing relationship (clients, vendors) → Professional-warm. If internal (direct reports, core team) → Casual-professional. If ambiguous → default to Professional-warm.

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

**Decision sequence:**
1. **Does the user provide recipient, channel, or tone preference?** → Use what they provide.
2. **Does the user request output-only mode?** (phrases: 「直接給」「只輸出結果」「just output」「skip explanation」) → Skip to Step 3, omit explanations.
3. **No context provided?** → Use defaults: recipient = peer/stakeholder, channel = email, tone = professional-warm.

**Example**:
- User: "Polish this email to my client about project delays"
- Q1: Recipient/tone provided? Yes (external client mentioned)
- Q2: Output-only? No
- → Recipient formality: Client = Professional-warm
- → Proceed to Step 2

### 2. Diagnose Priority Issues

**Exact procedure:**
1. Read the entire draft once.
2. Mark which issue types (from table below) are present. Use top-to-bottom table order as priority rank.
3. Count total issue types found.
4. **If 3 or fewer issue types present** → Address all of them in Step 3.
5. **If more than 3 issue types present** → Address only the first 3 in table order. Then ask user: "The following issues remain: [list]. Which should I prioritize?"

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

**For normal mode:**
- **Polished version** in blockquote (copy-paste ready):
  > [polished message]
- **Change notes**: One line per change.
  - Format: `[line X, phrase "xxx"] issue-type: original → polished (reason)`.
  - Example: `[line 3, phrase "可能也許"] hedging-overload: 「可能也許」→ removed (commit to timeline)`.
  - Each note: under 20 words.

**For output-only mode:**
- Polished message in blockquote only.
- Single assumption line: `Assumed: recipient=[role], channel=[email/LINE/etc], register=[formal/professional-warm/casual-professional]`.
- No change notes. No explanation.

### 4. Respond to Feedback

Accept refinements and re-output in same format as Step 3 (normal or output-only, whichever was used initially).

## Constraints

### Scope Gate (Evaluate First)

Decline and recommend another skill for:
- Translating to another language (use translator skill).
- Creating new content from scratch (use content-writer skill).
- Legal or compliance review (refer to legal counsel).
- Applying corporate style guide, AP style, or external brand standards (use branding skill).
- Messages where the main goal is tone-shifting without content refinement (use brainstorming skill instead).

If the draft falls into any of these categories, state the category and suggest the alternative. **Evaluate scope before proceeding to Step 1.**

### Constraint Priority Hierarchy

If constraints appear to conflict, resolve in this order:
1. **Scope Gate** — Never proceed if request falls outside scope.
2. **Register Lock-in** — Once set, preserve register unless user explicitly requests shift.
3. **Paraphrase Depth** — Content integrity (main subject, key commitment, intent) takes precedence over stylistic polish.
4. **Length** — ±15% word count rule applies unless user explicitly requests expansion/compression.
5. **Voice** — Author's personality and tone are preserved above mechanical refinement.
6. **Format Stability** — Once delivered, structure is maintained in all revisions.

### Recipient Formality Map

Use this to determine register when recipient is specified:
- **Formal**: Legal stakeholders, government, senior external executives, compliance officers, first-time external contacts.
- **Professional-warm**: Clients, vendors, internal directors, colleagues across teams.
- **Casual-professional**: Direct reports, core team members, long-term collaborators with established rapport.

### Register Lock-in

Once register is determined in Step 1, do not shift it in subsequent versions unless the user explicitly requests a register change. If refinements could push toward a neighboring register, stay within the locked register.

### Tone Drift Tolerance

Tone must not shift more than one level on the Tone Spectrum in a single pass. (Cannot jump from Formal to Casual-professional.) If user feedback indicates a two-level shift is needed, ask: "This would shift from [register A] to [register C]—is this intentional?"

### Output-Only Mode (Delivery Guarantee)

When the user requests "直接給", "只輸出結果", "output only", or similar, never substitute a question for the deliverable — deliver the polished message immediately without asking. Record assumptions as one line: `Assumed: recipient=X, channel=Y, intent=Z`.

### Assumption Transparency (Mandatory)

State all assumptions about recipient, channel, and register whenever they are inferred rather than provided. Format: `Assumed: recipient=[role], channel=[email/LINE/etc], register=[formal/professional-warm/casual-professional]`.

This applies in both normal and output-only modes. No assumption is implicit—all must be surfaced.

### Paraphrase Depth

Preserve all main subjects and key commitments. Define "fundamental content" as: (1) primary subject, (2) key commitment or promise, (3) stated intent. If changing more than 2 of these 3, ask the user which to prioritize.

### Length

Polished version must be within ±15% of original word count.

### Content

Rephrase only. No facts added, removed, or invented.

### Voice

Preserve author's personality, phrases, idioms, and humor. Remove: filler words ("basically", "like"), hedging language ("maybe", "probably"), redundant apologies.

### Format Stability

After initial blockquote delivery, maintain the same line breaks and paragraph structure in all subsequent versions.

### One-Question Rule

Ask at most one clarifying question per exchange. Always provide a best-guess default.

### Iteration Stopping Rule (Mandatory)

**When to stop iterating:**
1. After 2 revisions on the same issue type within one exchange, ask: "Which specific aspect of [issue-type] should I focus on?" Do not revise a third time without explicit direction.
2. If user indicates satisfaction ("looks good", "perfect", "thanks", "done"), deliver final version. Offer further adjustments only if user initiates.
3. If user requests fundamental restructuring (not polish), acknowledge and recommend escalation: "This goes beyond polish—I'd recommend a design or brainstorming skill instead."

### Iteration Protocol

When user requests a second round of corrections for the same issue type, ask for explicit direction before re-polishing: "Which specific aspect of [issue-type] should I focus on?" Do not assume what the user wants.