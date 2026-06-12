# lenny-episode-capture

A Claude Agent Skill that captures a single [Lenny's Newsletter](https://www.lennysnewsletter.com/)
episode (podcast interview or written post) into a faithful, structured **bilingual
(English + 中文)** raw-material document.

## What it does

Given one episode, it reads the full transcript end to end and produces:

- a Chinese **TL;DR**
- **themes**, each with a bilingual one-line headline, the guest's **argument structure
  (▸)** — why / thresholds / qualifications / anti-patterns / procedures, as the guest
  stated them — concrete **examples (📎)**, **verbatim quotes with timestamps (📌)**,
  and an optional neutral **tension flag (⚖️)**
- light subject-matter **tags** and a one-line summary

## The one design principle: capture, never judge

This skill produces **raw material only**. It deliberately does *not* rank themes by
importance, write recommendations or action items, or tell you what to conclude. Those
judgments belong to a separate, human, downstream step — and keeping them out is what
preserves the document's fidelity and makes the capture safe to automate.

If you want a tool that hands you "the 3 key takeaways," this isn't it, by design. It
hands you trustworthy raw material so *you* can do the thinking.

## Requirements

- **A connected Lenny content source (MCP / connector)** is the primary, highest-fidelity
  input: the skill resolves the episode and reads the full text through it. Without one,
  it falls back to fetching the episode URL directly (lower fidelity, possibly partial).
- **A strong model.** Verbatim quoting across a long transcript is demanding; weaker
  models tend to paraphrase quotes as if exact, or silently drop late-episode content.

## Install

This is an [Agent Skill](https://docs.claude.com). Add it as a custom skill (e.g. in
Claude Cowork's skill settings) by uploading the skill folder as a ZIP. See Anthropic's
current documentation for the exact install steps, which may change.

## Usage

Just ask, for example:

- "Capture the latest Lenny episode."
- "Run the capture on `<Lenny episode URL>`."
- "Turn this Lenny transcript into the raw layer."

## Output shape

Each theme is captured as:

```
## Theme N — <EN title> / <中文标题>
**Headline:** <one EN sentence> / <一句中文>
▸ **论证 / Structure:** <the guest's own reasoning: why / threshold / qualification / anti-pattern / procedure>
📎 **例证 / Examples:** <concrete instances the guest cited, if any>
> 📌 **Original:** "<verbatim quote>" (<timestamp>)
⚖️ 张力: <one neutral line, only where the claim is genuinely contestable>
```

## Adapting it

- **Language conventions:** bilingual (EN + 中文) is used only for retrieval anchors
  (titles, per-theme headlines, the one-line takeaway); quotes stay in English; all
  exposition (Structure, examples, tension flags, TL;DR) is compact Chinese with proper
  nouns in English. These conventions live in one section of `SKILL.md` — to ship a
  fully-English variant, that is the one place to change.
- Tags are descriptive subject-matter only (`#hardware`, `#consumer-ai`, …) — never
  importance scores or "what skill this builds." Mapping content to your own development
  goals is downstream work this skill stays out of on purpose.

## What it intentionally leaves out

This is the *capture* layer of a larger personal learning workflow. The synthesis layer —
deciding what matters, connecting it to your own work, and what to do about it — is kept
human by design and is not part of this skill.

## License

[MIT](./LICENSE).

## Changelog

See [CHANGELOG.md](./CHANGELOG.md).
