# Lenny Episode Capture — ChatGPT, Codex & Claude

A portable Agent Skill that captures a single [Lenny's Newsletter](https://www.lennysnewsletter.com/)
episode (podcast interview or written post) into a faithful, structured **bilingual
(English + 中文)** raw-material document. The same `SKILL.md` follows the open
[Agent Skills specification](https://agentskills.io/specification) and runs unchanged in
ChatGPT, Codex, and Claude.

## What it does

Given one episode, it reads the full transcript end to end and produces:

- a compact **source manifest** recording provenance, completeness, and whether the full
  source was retained
- a Chinese **TL;DR**
- **themes**, each with a bilingual one-line headline, the guest's **argument structure
  (▸)** — why / thresholds / qualifications / anti-patterns / procedures, as the guest
  stated them — concrete **examples (📎)**, **verbatim quotes with timestamps (📌)**,
  and an optional neutral **tension flag (⚖️)**
- light subject-matter **tags** and a one-line summary

When the host supports files and the source can be retained, the Skill saves the complete
transcript/post as a **separate audit artifact**. It never embeds the full source inside
the C1 capture.

## The one design principle: capture, never judge

This skill produces **raw material only**. It deliberately does *not* rank themes by
importance, write recommendations or action items, or tell you what to conclude. Those
judgments belong to a separate, human, downstream step — and keeping them out is what
preserves the document's fidelity and makes the capture safe to automate.

If you want a tool that hands you "the 3 key takeaways," this isn't it, by design. It
hands you trustworthy raw material so *you* can do the thinking.

## Requirements

- **A complete source text.** A connected Lenny source is the highest-fidelity option;
  otherwise provide a full transcript/post or an episode URL the current platform can
  read in full. The skill stops rather than claiming complete coverage from a partial page.
- **A strong model.** Verbatim quoting across a long transcript is demanding; weaker
  models tend to paraphrase quotes as if exact, or silently drop late-episode content.

## Install

Use the same `lenny-episode-capture` folder on every host. Platform-specific files such
as `agents/openai.yaml` only add host UI metadata; they do not change the workflow or
create a dependency on that platform.

### ChatGPT

In the ChatGPT desktop app, open **Skills** in the sidebar and import the
`lenny-episode-capture` folder or packaged ZIP. Invoke it with
`@lenny-episode-capture`, or ask for a matching Lenny capture and let ChatGPT select it.

### Codex

For a personal Skill, copy or symlink the folder to:

```text
~/.agents/skills/lenny-episode-capture/
```

For a repository-scoped Skill, use:

```text
<repo>/.agents/skills/lenny-episode-capture/
```

Codex detects changes automatically; restart only if it does not appear. Invoke it with
`$lenny-episode-capture`, or let Codex select it from the request.

### Claude

In Claude, open **Customize → Skills → + → Create skill → Upload a skill**, then upload
the packaged ZIP. The ZIP contains the `lenny-episode-capture/` folder at its root, as
Claude expects.

For Claude Code, copy or symlink the same folder to either:

```text
~/.claude/skills/lenny-episode-capture/
<repo>/.claude/skills/lenny-episode-capture/
```

Invoke it with `/lenny-episode-capture`, or let Claude select it automatically.

## Usage

Just ask, for example:

- "Capture the latest Lenny episode."
- "Run the capture on `<Lenny episode URL>`."
- "Turn this Lenny transcript into the raw layer."

Explicit invocation syntax differs by host—`@lenny-episode-capture` in ChatGPT,
`$lenny-episode-capture` in Codex, and `/lenny-episode-capture` in Claude Code—but the
Skill instructions and output are identical.

## Output shape

A file-capable run produces:

```text
source-manifest.md     required
transcript.md          conditional: only when retention is supported and permitted
c1-capture.md          required
```

Generated episode data belongs in the user's chosen project or workspace, **not in this
Skill repository**. The manifest records a stable retrieval reference when the full source
cannot be retained. The C1 capture remains the default downstream reading surface; the
complete source is consulted only to verify omissions, context, qualifications, examples,
or quotations.

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

It also leaves personal learning artifacts out of the public Skill repository: transcripts,
real episode captures, downstream notes, and competency ledgers should remain in the user's
own workspace unless explicitly prepared as rights-safe public examples.

## License

[MIT](./LICENSE).

## Changelog

See [CHANGELOG.md](./CHANGELOG.md).
