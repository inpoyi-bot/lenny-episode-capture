# Changelog

All notable changes to this skill are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/), and this project
adheres to [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Added
- Added `agents/openai.yaml` UI metadata for ChatGPT and Codex.
- Added installation and invocation guidance for Codex and Claude Code.
- Added a single cross-platform upload package with the Skill folder at the ZIP root.
- Added a required source manifest for provenance, completeness, closing verification,
  transcript-retention status, and downstream retrieval.
- Added an optional separate full-source artifact when the runtime and source conditions
  permit retention.

### Changed
- Made source resolution platform-neutral: use the current environment's connected source,
  a user-supplied full transcript, or a URL only when it yields complete text.
- Added ChatGPT installation guidance and removed the Claude-only packaging assumption.
- Shortened the trigger description to 199 characters so it satisfies Claude's stricter
  custom-Skill metadata limit while retaining the main positive and negative triggers.
- Defined the C1 capture as the default downstream input and the full transcript/post as an
  audit artifact used only for source verification.
- Prohibited writing generated transcripts, captures, manifests, or personal downstream
  notes into the reusable Skill repository unless explicitly requested as rights-safe tests.

## [1.1.0] - 2026-06-12

Driven by the first real eval: an independently produced human baseline (the user's own
full-listen notes) diffed against the skill's output on the same episode. The systematic
gap: the skill captured conclusions but dropped the guest's reasoning around them.

### Added
- `▸ 论证 / Structure` block per theme: captures the guest's own argument — why,
  thresholds, qualifications, anti-patterns, procedures — with the same omit-don't-invent
  discipline as `📎`/`⚖️`. Conclusion-only capture is now treated as a fidelity loss.
- Mining step in the procedure: re-scan each substantive answer for independent claims
  beyond its headline (one-answer-one-point identified as the main silent-loss mode).
- Optional descriptive part headers when the episode has a clear narrative arc
  (content grouping is description; importance ranking remains forbidden).
- Guest-made cross-theme links may be recorded descriptively; capturer-noticed links
  remain the reader's layer.

### Changed
- Language conventions consolidated and simplified: bilingual only for retrieval anchors
  (titles, one-sentence headlines, one-line takeaway); quotes English-only; all
  exposition in compact Chinese. The parallel 2–4-sentence EN/中文 theme bodies are
  removed as zero-information duplication.
- Worked example replaced with one demonstrating headline + Structure capture.
- Checklist extended accordingly.

## [1.0.0] - 2026-06-10

### Added
- Initial release: capture a single Lenny's Newsletter episode into a faithful,
  structured bilingual (English + 中文) raw-material document.
- Full (100%) transcript read, with verbatim quotes and timestamps; transcription
  artifacts flagged inline rather than silently "fixed."
- Primary input via a connected Lenny content MCP (search/list to resolve the episode,
  read to pull the full text); direct URL fetch as a documented fallback.
- Per-theme structure: English point, 中文 point, `📎` examples, `📌` verbatim quote,
  and an optional neutral `⚖️` tension flag.
- "Capture, never judge" boundary enforced at three layers (role definition, hard
  boundary list, and a worked example): no ranking, no recommendations, no action items.
- Descriptive subject-matter tags, explicitly defined as *not* competency or
  importance labels.
