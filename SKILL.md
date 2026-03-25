---
name: message-polish
description: "Message Polish"
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

Refine draft messages into professional yet warm business communication.
Preserve the author's voice and intent — only fix what's unprofessional, awkward, or unclear.

## Agent Delegation

This skill runs entirely in main context. Polishing is a single-pass reasoning task
that benefits from conversational back-and-forth; delegation adds overhead without value.

## Core Principles

### Scope Boundaries
- **Polish**: Fix tone, clarity, flow, redundancy, passive-aggressive undertones
- **Preserve**: Keep the author's personality, intent, warmth, and key information
- **Explain**: Every change gets a brief reason (not just "sounds better")
- **NOT generate**: Creating new content from scratch → use `content-writer`
- **NOT translate**: Cross-language translation → direct request
- **NOT marketing**: Ad copy, campaigns → use `marketing-copy`

### Tone Spectrum

| Register | When | Example Context |
|----------|------|-----------------|
| **Formal** | Contracts, legal clauses, official notices | 報價單條款、合約文字 |
| **Professional-warm** | Client messages, business emails | LINE 訊息、Email（**default**） |
| **Casual-professional** | Internal team, familiar collaborators | 同事間訊息、Slack |

## Workflow

### 1. Analyze

Identify from the draft: **recipient** (client/partner/team), **channel** (LINE/Email/doc),
**relationship** (formal/established/familiar), **intent** (what the author wants to achieve).

### 2. Diagnose

Scan for these problems in priority order:

| Issue | Example | Fix Pattern |
|-------|---------|-------------|
| Passive-aggressive | 「否則承辦方將自行購買」 | Reframe as neutral options |
| Presumptuous | 「你應該也比較放心」 | Remove assumptions about feelings |
| Buzzword/cliché | 「雙贏」「共創價值」 | Replace with specific, honest language |
| Run-on topics | Business + personal in one breath | Split with natural transition |
| Hedging overload | 「可能也許大概應該…」 | Commit to a stance |
| Redundancy | Same thing said twice | Keep the stronger version |
| Register mismatch | Formal + slang mixed | Unify tone |

### 3. Output

Always produce both:

**Polished version** in a blockquote (ready to copy-paste):

> [polished message]

**Change notes** — one line per change: what → why. Keep concise.

### 4. Iterate

- 「太正式」/ 「太硬」/ 「不像我」→ dial back
- 「還是口語」/ 「再專業一點」→ tighten
- Track preference within the session

## Quick Reference: Chinese Business Pitfalls

| Avoid | Use Instead | Why |
|-------|-------------|-----|
| 你應該… | (remove or soften) | Don't tell them how they feel |
| 麻煩你… | 能否協助… / 方便的話… | Less subservient, more peer-level |
| 否則… | 亦可由… | 「否則」carries threat undertone |
| 雙贏 | 互利合作 / 各取所長 | Overused to meaninglessness |
| 幫助你的公司 | 幫到公司 | Less patronizing |
| 確定這是你要的 | 確認方向對了 | Don't imply doubt |
| 歡迎+命令 | 分開：邀請+說明 | 「歡迎協助代購」= inviting them to do your errand |
