---
name: lenny-episode-capture
description: "Capture one Lenny episode/post as bilingual raw material: themes, reasoning, examples, and timestamped quotes from the full text. Use for Lenny links, titles, guests, or latest. Never rank or advise."
---

# Lenny Episode Capture (C1 raw-material layer)

## What this skill is for — and the one rule that defines it

Produce a faithful, structured **raw-material** document from **one** Lenny's Newsletter
episode. That is the entire job. The output is the input to a separate human step
(the reader picks what matters, connects it to their own work, and decides what to do).

**The defining rule: capture, never judge.** This skill must not prioritize themes,
write recommendations or action items, or tell the reader what to conclude or do.

Why this rule matters enough to be the skill's identity:
- The learning happens when the *reader* does the prioritizing and the "so what for me."
  If this skill does that work, it silently steals the most valuable step.
- The raw layer's only value is fidelity. The moment it editorializes, a downstream
  reader can no longer tell the speaker's claim apart from the capturer's opinion — a
  "confident error" that propagates with no signal and cannot be debugged later.
- Keeping the layer clean is what lets the capture be automated/scheduled while the
  judgment stays human. Blur the line and you can no longer safely automate it.

If at any point you find yourself wanting to write "the reader should…", "the key
lesson is…", or to mark one theme as more important than another — **stop. That is the
reader's layer, not yours.**

## Scope

- **One episode per run.** Do not synthesize across episodes or compare guests — that
  is a separate, downstream activity.
- **Not** the "what should I do" layer (no advice, no takeaways for any audience).
- Does not verify claims, fact-check the guest, or assess whether advice is good. It
  only flags where a claim is *contestable* (see "Tension flags"), as neutral raw
  material for the reader to judge.

## Inputs and cross-platform source strategy

Use the best source available in the current environment. Do not depend on a provider-
specific tool name, UI, connector, invocation syntax, or storage location. Treat
platform-specific metadata outside this file as optional host configuration, never as a
runtime dependency.

**Source priority:**
1. A connected Lenny content source that can search/list episodes and read the complete
   transcript or post.
2. A complete transcript or post text supplied by the user as a file or in the chat.
3. The episode URL, only when the current environment can retrieve the complete text.

The connected source is normally the highest-fidelity option; prefer it over a web page
that may be truncated or paywalled.

**Mandatory runtime discovery and fallback gate:** Before using a supplied or discovered
URL, actively inspect the tools/connectors available in the current runtime for a Lenny
content source (including a Lenny MCP or an equivalent connected source). If one is
available, you **must invoke it first** to resolve the episode and request the complete
transcript or post. Do not skip the connected source merely because a public URL is easier
to access. Fall back to input 2 or 3 only after confirming that no such source is available,
access is denied, or its search/read capability cannot return the complete text; state the
fallback reason in the run. Discover the source from actual runtime capabilities rather
than assuming or inventing a provider-specific tool name.

Accept any of these as the way the user points at an episode, then resolve it against the
source:
- A **URL** to a Lenny episode.
- An **episode title or guest name** (search/list the source to locate the match).
- **"The latest episode"** (list the source and take the most recent one).

Typical flow: use the available source's search/list capability to resolve the input to
exactly one episode, then use its read capability to pull the **full** transcript or post
text.

**Completeness gate.** If the accessible URL or source yields only a preview, excerpt, or
otherwise partial text, do not present a capture as 100% coverage. Ask the user to provide
the full transcript or enable a source with full access. Never fill a coverage gap from
memory, search snippets, or inference.

Before writing anything, **confirm the episode identity** — title, date, guest, link —
so the run is unambiguous and auditable.

## Model note

Verbatim quoting across an 18,000-word transcript is demanding: weaker/faster models
tend to paraphrase quotes while presenting them as exact, or drop late-episode content.
Run this on a strong model. Treat model choice as a quality variable, not a detail —
the fidelity of the output is inseparable from it.

## Procedure

1. **Identify and confirm the episode.** Resolve the input to one specific episode via
   the available source, and state its title, date, guest, and link. If
   "latest" is ambiguous or you cannot reach the source, say so rather than guessing.

2. **Read 100%, end to end.** Pull the full text through the available source or supplied
   transcript — not an excerpt or preview. Verify you actually have the whole thing through to the close
   (the final exchange / sign-off); if the read returns content in chunks, page through
   to the end. Partial reads silently drop late material, and the most pointed takes
   often come at the end — never let coverage trail off.

3. **Derive themes.** Group the substance into themes — as many as the content genuinely
   warrants, merging near-duplicates. Aim for roughly ≤ 15; do **not** force a target
   number, pad thin material, or split one idea to inflate the count. Keep themes in the
   order they best represent the episode (rough chronological or natural grouping) — do
   **not** order them by how important you think they are. Where the episode has a clear
   narrative arc, you **may** group themes under descriptive part headers (e.g. "what to
   build / how to decide / how to make people want it") — grouping by the episode's own
   content logic is description; ranking by importance is judgment.

4. **Write each theme** using the exact block in "Output template": a one-sentence
   bilingual **headline** (one EN sentence + 一句中文), a `▸ 论证 / Structure` block
   capturing how the guest's argument is built (see "Capture the argument" below), an
   `📎 例证 / Examples` block for the concrete instances cited, one or two verbatim
   quotes with timestamps, and — only where warranted — one neutral tension flag.

5. **Mine each substantive answer before moving on.** A long answer usually contains
   more than its headline claim — thresholds ("good enough to ship"), qualifications,
   anti-patterns, named procedures. Before finalizing, re-scan each substantive answer
   and ask: *besides the headline, what other independent claims did the guest make
   here?* Promote ones that stand alone to their own theme; fold supporting ones into
   that theme's Structure block. One-answer-one-point is the main way capture silently
   loses substance.

6. **Quote verbatim; flag artifacts; never clean up.** Quotes must be word-for-word from
   the transcript. Where the transcript clearly mis-transcribes a word, keep the original
   and flag the likely intended word inline (e.g. `"long-term laws" [likely "flaws"]`).
   Never fabricate, paraphrase-as-quote, or silently "fix" a quote. A polished-but-wrong
   quote is worse than a rough-but-true one, because nothing downstream signals the error.
   Keep each quote short and load-bearing; attach a timestamp (or `~mm:ss` estimate).

7. **Write the TL;DR** in Chinese, 3–5 sentences. It must be *descriptive* (what the
   episode covered), not *prescriptive* (what to do about it).

8. **Write the one-line summary** in both EN and 中文 — a faithful compression of the
   episode's throughline, still descriptive, no advice.

## The hard boundary — never cross into the reader's layer

Do **not**, anywhere in the output:
- Rank, score, star, or otherwise mark which themes matter most.
- Write recommendations, takeaways, "action items," "给新手 PM 的话," "你应该…",
  "建议你…," or any second-person instruction.
- Editorialize agreement or disagreement with the guest.
- Add a "my analysis" / "implications" / "how to apply this" section of any kind.

The only place your own framing is allowed is the **neutral tension flag** below.

**Self-check before finishing:** scan the whole document. If any sentence tells the
reader what to think or do, delete it. The reader's judgment is the point of the next
step; pre-empting it is the one way this skill fails.

## Capture the argument, not just the conclusion (▸ 论证 / Structure)

A theme's headline is a lossy compression of a *claim*; but guests rarely hand over bare
claims — they argue. The reasoning around a claim (why it holds, the threshold for acting
on it, the qualification that bounds it, the anti-pattern it warns against, the procedure
that operationalizes it) is load-bearing raw material **the guest actually said**.
Dropping it is the same fidelity loss as dropping an example: the reader receives a
conclusion they can neither weigh nor apply. In practice this is the single biggest way a
capture ends up shallower than the episode.

Rules for the `▸ 论证 / Structure` block:
- **Capture the argument's internal parts, one bullet per part, 0–5 per theme.** Typical
  parts: *why* (the stated reason), *threshold/criterion* (when it applies or is "enough"),
  *qualification* (the bound the guest themselves put on it), *anti-pattern* (the failure
  mode they named), *procedure* (the concrete how they described).
- **Only what the guest said.** Reconstruct their reasoning, never supply your own. If the
  guest gave a claim with no reasoning, the theme gets no Structure block — omit rather
  than backfill (same discipline as 📎 and ⚖️).
- **One line per bullet, compact Chinese, proper nouns in English** (same convention as 📎).
- **Distinct from 📎:** Structure is *how the argument is built*; 📎 is *which instances
  were cited*. Do not restate one in the other.
- **Guest-made cross-links are capture; yours are not.** When the guest explicitly ties
  this theme to another ("this is the same reason B2C is hard…"), record it descriptively
  inside Structure. Connections *you* notice belong to the reader's layer — leave them out.

## Language conventions (one place to change for an English variant)

The document uses each language for a distinct job:
- **Bilingual (EN + 中文)** only for retrieval anchors: document title, theme titles, the
  one-sentence headline per theme, and the one-line takeaway.
- **English** only for verbatim quotes (📌) — never translate them.
- **Compact Chinese, proper nouns kept in English**, for all exposition: TL;DR, Structure
  (▸), Examples (📎), and tension flags (⚖️).

Do **not** write parallel multi-sentence EN and 中文 expositions of the same content —
that duplicates information without adding any, and crowds out substance. To ship a
fully-English or fully-bilingual variant for open source, this section is the one place
to change.

## Examples block (📎) — capture the guest's concrete instances

A theme's point is a lossy compression; the guest's concrete example is the original.
Dropping it costs three things: the point gets harder to remember, harder to transfer to
the reader's own situation, and — most important — harder to falsify. An abstract
principle floating free of any instance is exactly where this kind of capture tends to
silently over-generalize or invent. Requiring each substantive theme to carry its
example forces the claim to stay evidence-backed and checkable. This is raw material
("what the guest cited"), not judgment, so it stays inside the skill's boundary.

Rules for the `📎 例证 / Examples` block:
- **Capture load-bearing specifics, not a retelling.** Name the real product / company /
  person, the specific decision or number, and the outcome — the parts that make the
  example *this* example. Skip narrative color.
- **One instance per bullet; 0–3 per theme.** A purely conceptual theme with no concrete
  instance gets no block — omit it rather than invent one (same discipline as ⚖️).
- **Compress, never interpret.** `Jobs decided on the virtual keyboard and told dissenters
  to leave` is fine; `this shows PMs should trust taste over data` is the reader's layer —
  forbidden here.
- **Do not fabricate.** Names, numbers, and outcomes are held to the same faithfulness bar
  as verbatim quotes. If you are unsure a detail is in the source, leave it out.

Keep the `📎` block distinct from the `📌` quote: the examples block is *what happened*
(a compact paraphrase of the instance); the quote is the guest's verbatim punchline. Do
not restate the same content in both.

- Good: `📎 例证:iPhone 实体 vs. 虚拟键盘是全场最久最激烈的辩论;两边数据 a wash,Jobs 拍板走虚拟,并让不服的人离开房间。`
- Bad (retelling + interpretation): `📎 例证:他们花了很多时间讨论键盘,这告诉我们好的 PM 要敢于拍板。`

## Tension flags (⚖️) — what they are and are not

A tension flag is *raw material for the reader's own critical read*, not your verdict.
Add one (one line, optional) only where a claim is genuinely contestable — e.g. it
likely reflects survivorship bias, depends on a specific context to hold, or runs
against common practice. State the condition, not a judgment.

- Good: `⚖️ 张力:此论断带明显幸存者偏差(讲者本人即少数成功者);在缺乏强势话语权的团队里照搬"无视数据靠品味拍板"风险高。`
- Bad (a verdict): `⚖️ 我觉得他这点是错的,数据其实很重要。`

Most themes need no flag. Do not manufacture tension to fill the slot.

## Tags (标签) — light, descriptive, subject-matter only

Tags are for archival retrieval, nothing more. Emit 3–6 tags, lowercase and hyphenated,
describing **what the episode is about** — its domain, industry, or career topic
(e.g. `#hardware` `#consumer-ai` `#founder-story` `#hiring` `#fundraising`
`#design-process`).

- Describe the **content**, not the reader. Tags say what the episode covers, never how
  important it is, what lesson to draw, or which PM skill it "develops" — mapping content
  to a competency or development goal is the reader's downstream judgment, not capture.
- Reuse stable tags across episodes so the archive stays searchable; do not coin a
  near-duplicate of an existing tag.

## Output template (use this exact structure)

```
# <英文标题> / <中文标题>

**Episode / 单集:** <title>
**Date / 日期:** <YYYY-MM-DD> · **Length / 篇幅:** ~<n> words
**Source / 来源:** <url>

**标签 / Tags:** `#topic-1` `#topic-2` … (3–6 个,描述主题/领域,非能力标签)

> 覆盖说明:本摘要基于对完整文字稿的 100% 阅读。引用逐字摘自<转写稿/原文>;
> 转写瑕疵(如有)已就地标注。

---

## TL;DR(纯中文,描述性,3–5 句)
<...>

---

# Part I — <描述性分节标题>(optional; only when the episode has a clear arc)

## Theme 1 — <EN title> / <中文标题>

**Headline:** <one EN sentence> / <对应一句中文>

▸ **论证 / Structure:**(仅当嘉宾给出了论证;0–5 条,一行一条,紧凑中文、专有名词留英文;否则省略)
- why:<嘉宾给出的理由>
- threshold:<何时适用 / 何为"够了">
- qualification:<嘉宾自己加的限定>
- anti-pattern:<嘉宾点名的失败模式>
- procedure:<嘉宾描述的具体做法>

📎 **例证 / Examples:** <仅当嘉宾给了具体实例时;0–3 条,中文密写、专有名词留英文;否则省略>
- <一条具体例证:真实的产品/公司/人 + 那个具体决策或数字 + 结果>

> 📌 **Original:** "<verbatim quote>" (<timestamp>)
>
> "<optional second verbatim quote>" (<timestamp>)

⚖️ 张力:<仅在确有可争议处加一行;否则省略>

---

## Theme 2 — …
(Repeat as needed. Order themes by content, not by importance. Structure bullets need not
use all five part-labels — only the parts the guest actually argued. Never add any
"advice / action item / 给…的话" block.)

---

## One-line takeaway / 一句话总结
**EN:** <descriptive one-liner>
**中文:** <对应中文>

---

*Source: <title>, Lenny's Podcast/Newsletter, <date>. <url>*
```

## Example (one theme block, showing the intended shape)

```
## Theme 1 — Opinion-based decisions & taste makers / 1.0 靠"观点决策"与品味决策者

**Headline:** A true 1.0 has no analogs, so most decisions must be opinion-based, made
by one or two empowered taste makers. / 全新品类的 1.0 没有可参照对象,大多数决策只能
基于观点,由一两个被授权的"品味决策者"拍板。

▸ **论证 / Structure:**
- why:硬要数据只有两条死路——要么从别的品类硬搬数据(那就不差异化了),要么拿到 "bullshit data"。
- threshold:拍板的判据不是"最好"而是 "good enough to ship"——虚拟键盘不如实体好,但够好,先发出去拿真反馈。
- qualification:"informed gut" ≠ 拍脑袋——前面有大量专家输入、提问、prototype,最后才由少数人拍那一刀。
- qualification:对没有 Jobs 式权威的人,他给的替代是把 why 讲清楚到能把所有人带动起来(articulate the informed gut)。
- anti-pattern:大公司请咨询、做 user study,只为"证明 1.0 会成功"——用假数据 cover their ass,而不是承担决策。

📎 **例证 / Examples:**
- iPhone 实体 vs. 虚拟键盘:全场最久最激烈的辩论;数月软硬件测试后数据胶着(a wash),
  Jobs 拍板走虚拟,并让不服的人离开房间。

> 📌 **Original:** "if you try to do data-driven decisions all the way along, you're
> either not doing a differentiated product… or you're just getting just bullshit
> data." (~00:07:30)
>
> "Were we as good as a hardware keyboard? No. But were we good enough? Yes." (~00:09:10)

⚖️ 张力:此论断带明显幸存者偏差(讲者本人即少数成功案例);在缺乏强势话语权或深厚领域
直觉的团队照搬"无视数据靠品味拍板",风险较高。
```

(Note the Structure block carries the guest's own reasoning — thresholds, qualifications,
anti-patterns — not the capturer's analysis; and there is no "💡 给新手 PM 的话," no
ranking, no advice. Both disciplines together are exactly what this skill enforces.)

## Before you finish — quality checklist

- Episode identity confirmed (title / date / guest / link)?
- Coverage reached the actual end of the transcript (no silent trailing-off)?
- Every quote verbatim, short, timestamped; transcription artifacts flagged in place?
- Themes ordered by content, **not** by importance; no theme marked as more important?
- Does every theme that rests on a concrete instance carry a checkable `📎` example
  (real product/company/person, the specific decision or number, the outcome)? None
  fabricated or padded; none that merely retell or interpret?
- Does every theme where the guest *argued* (gave a why, threshold, qualification,
  anti-pattern, or procedure) carry that reasoning in `▸ Structure` — and is every
  Structure bullet something the guest actually said, not your reconstruction?
- Did you re-scan each substantive answer for claims beyond its headline (thresholds,
  anti-patterns, procedures) before finalizing?
- **Zero** recommendations, takeaways, action items, "给…的话," or second-person advice?
  Any cross-theme links recorded only where the guest made them explicitly?
- Tension flags (if any) state a condition, not a verdict; none manufactured?
- Language conventions held: bilingual only for titles/headlines/one-liner; quotes in
  English untranslated; all exposition in compact Chinese; no parallel EN/中文
  duplication of the same content?
