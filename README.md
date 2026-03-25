[English](README.md) | [繁體中文](README.zh.md)

# Message Polish

A Claude Code skill that refines draft messages into professional yet warm business communication. It preserves the author's voice and intent — fixing only what is unprofessional, awkward, or unclear — and explains every change with a brief reason.

## Features

- Three-register tone spectrum: Formal, Professional-warm (default), and Casual-professional
- Diagnoses seven common problems: passive-aggressive phrasing, presumptuous assumptions, buzzwords, run-on topics, hedging overload, redundancy, and register mismatch
- Outputs a ready-to-copy-paste polished version alongside annotated change notes
- Iterative refinement: dial tone up or down based on feedback ("too formal", "still too casual")
- Chinese business communication pitfall guide with specific before/after substitutions
- Session-level preference tracking for consistent tone across multiple messages

## Usage

```
/message-polish
```

Trigger phrases: paste a draft message and ask to polish it, "幫我潤飾這則訊息", "改一下這封 email", "讓這段文字更專業", or simply share the draft text.

## How It Works

The skill identifies the recipient, channel, relationship, and intent from the draft, then scans for tone and clarity issues in priority order. It produces a blockquote-formatted polished version and a concise list of change notes explaining what was altered and why — not just "sounds better". Subsequent back-and-forth adjustments are tracked within the session to maintain consistency.

## Requirements

- Claude Code CLI

## License

MIT
