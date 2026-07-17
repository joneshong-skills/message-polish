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
**Preserve**: Author's personality, intent, and key information. Retain warmth and humor from the original where appropriate.
**Explain**: Every change with a brief reason (under 20 words).

## Constraints

- **Context sufficiency**: Infer recipient (client/partner/team), channel (LINE/Email/document), and intent (request/update/negotiation/proposal) from the draft and the request itself (salutation, register, stated purpose). Record inferences as assumptions in the change notes. Ask only when a remaining ambiguity would change the Tone Spectrum register — one question at a time, with a best-guess default attached.
- **Paraphrase depth**: Preserve all main subjects and key commitments. Tone shifts must not exceed one level on the Tone Spectrum. If achieving the desired tone requires changing more than 3 fundamental message elements, ask user to prioritize which changes are essential.
- **Length**: Within ±15% of original word count.
- **Content**: Rephrase only. No facts added, removed, or invented.
- **Voice**: Preserve author's personality, phrases, idioms, and humor. Remove only: filler words ("basically", "like"), hedging language ("maybe", "probably"), and redundant apologies.
- **Issue scope per pass**: When the message contains ≤3 issue types, address all in order. When it contains >3 issue types, address the first 3 (in table order), then ask user which remaining issues to prioritize.
- **Iteration convergence**: After 2 complete iterations on the same issue type, stop and ask for specific direction before attempting a third iteration.
- **Format stability**: After the initial blockquote delivery, maintain the same line breaks and paragraph structure in all subsequent versions.
- **When to decline**: Decline and recommend the correct skill if the task is: translating to another language, creating new content (not refining existing), legal or compliance review, or applying an external style guide.

## Tone Spectrum

| Register | Context | Language Marker | Constraint |
|----------|---------|-----------------|-----------|
| **Formal** | Contracts, legal, official notices | "Please proceed per the specified terms" | No colloquialisms; strict grammar; minimal personality |
| **Professional-warm** | Client messages, emails | "Let's get this done on schedule—happy to help" | Balance professionalism with approachability (default) |
| **Casual-professional** | Internal team, familiar collaborators | "Let's wrap this up by EOW" | Conversational yet clear; informal OK if unambiguous |

Identify the register before polishing; do not shift without explicit request.

## Workflow

### 1. Identify Context

Determine recipient, channel, and intent from what the draft and the request already reveal (salutation, register, stated purpose). Ask only about what remains genuinely ambiguous AND would change the Tone Spectrum register — one question at a time, with a best-guess default. When the user asks for output only, never substitute a question for the deliverable: polish under the most reasonable reading and append one line "Assumed: recipient=X, channel=Y, intent=Z".

Example: "This is an email to Client X about contract renewal. Intent: maintain warmth while setting a clear deadline."

### 2. Diagnose Priority Issues

Identify which issue types from the Priority Issues table are present in the message. If ≤3 types, address all. If >3 types, address the first 3 (in table order), then ask user which remaining issues to prioritize.

| Issue | Example | Fix Rule |
|-------|---------|----------|
| Passive-aggressive | 「否則承辦方將自行購買」 | Reframe as neutral options |
| Presumptuous | 「你應該也比較放心」 | Remove assumptions about recipient's feelings |
| Cliché | 「雙贏」「共創價值」 | Replace with specific language |
| Run-on topics | Work topic + personal chat without transition | Split with natural transition |
| Hedging overload | 「可能也許大概…」 | Commit to a stance |
| Redundancy | Same thing said twice | Keep the stronger version |
| Register mismatch | Formal language + casual phrases mixed | Unify tone |

### 3. Output Format

**Polished version** in blockquote (copy-paste ready):

> [polished message]

**Change notes**: One line per change. Format: `[line X, phrase "xxx"] issue-type: original → polished (reason)`.

Example: `[line 3, phrase "可能也許"] hedging-overload: 「可能也許」→ removed (commit to timeline)`.

Each note under 20 words. Reference the original phrase from the message in quotes. Issue type must match the Priority Issues table.

### 4. Iterate on Feedback

When the user provides feedback on the same issue type a second time, ask them to specify which aspect they want to focus on next, rather than attempting another iteration unprompted.

## Chinese Business Pitfalls

| Avoid | Use Instead |
|-------|-------------|
| 你應該… | (remove or soften — don't prescribe feelings) |
| 麻煩你… | 能否協助… / 方便的話… |
| 否則… | 亦可由… |
| 雙贏 | 互利合作 / 各取所長 |
| 幫助你的公司 | 幫到公司 |
| 確定這是你要的 | 確認方向對了 |