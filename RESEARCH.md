# Scope notes | 23 November 2026

## Choice

A manual local SRT review desk with optional video and a note report. It keeps decisions with the reviewer. It does not pretend that a reading-speed number proves subtitle quality or that this category is new.

## Sources read

- Community discussion: https://github.com/laubonghaudoi/subtitle-editor/issues/34 . Historical request/discussion of readability metrics and subtitle guidance. Useful motivation, not proof that the need is still unserved. No contribution or outreach is part of this project.
- Existing implementation: https://github.com/Ax1zz/cuelint . Already offers broad offline subtitle linting, including a standalone browser tool. A generic linter would duplicate it.
- Existing implementation: https://github.com/AresE87/srt-check . Another local SRT checking/reporting option. CueDesk instead puts reviewer notes and optional video navigation beside cues.
- Delivery guidance: https://studiopartner.netflix.net/studio/us-english-timed-text-style-guide . Source-specific English guidance includes adult reading-speed and line-length values. CueDesk's editable defaults are examples only; it does not implement a Netflix profile or claim compliance. Grapheme counting is an explicit implementation choice, not asserted equivalence with a delivery spec.
- Framework documentation: https://vuejs.org/guide/introduction.html . Vue's declarative/reactive UI model fits in-tab review state. Vue is bundled so end users need no package installation.
- Platform documentation: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/Segmenter . Grapheme segmentation avoids counting a combining mark or joined emoji as multiple visible characters. Browser support is required; no silent code-point fallback is used.
- Platform documentation: https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/currentTime . Local video seeking uses this browser property. Approximate cue-end stopping uses time updates, so no frame-accurate or synchronization claim is made.

## Deliberate limits

Basic SRT only; no font/style parser, automatic edits, translation, speech analysis, report import, or durable storage. A report omits caption text but cannot sanitize private text a reviewer types in notes. Unknown video codec/device behavior is reported honestly. Defaults can be changed and must be evaluated for the content, language, audience and delivery requirements.
