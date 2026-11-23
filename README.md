# CueDesk

<img src="logo.svg" width="72" alt="N inside a subtitle frame">

A small local subtitle review desk built with Vue. Open an SRT, optionally open a local video, move through cues, and record what needs another look in your subtitle editor.

**Free, no account, no hosted service.** The bundled `cuedesk.html` runs locally. It has no analytics, external fonts, or runtime network requests. Vue is bundled with its MIT notice.

## Use

1. Download the repository ZIP using GitHub's **Code > Download ZIP**, then extract it.
2. Open `cuedesk.html` in a recent desktop browser. Chrome/Chromium was tested.
3. Open a basic UTF-8 SRT file, paste one, or choose **Fictional demo**.
4. Optional: open a local video in a browser-supported codec. Cue selection seeks; **Play this cue** stops approximately at its end. This uses browser time updates, not frame-accurate controls.
5. Review flagged or unflagged cues. Record **Keep after review** or **Revisit**, and a note.
6. Build a JSON review report, inspect what you wrote, check the acknowledgment, and download it.

There is no autosave. Reloading, starting a new review, or clearing the review loses current notes. Keep your report before leaving. Reports cannot be imported back into CueDesk in this version. Original SRT/video files are never modified.

## What it measures

- Editable reading-load, line-length, and short-duration flags. Defaults are examples, not a delivery profile.
- Grapheme clusters using `Intl.Segmenter`, including spaces/punctuation, excluding line breaks. This can differ from platform character-count definitions.
- Literal markup is counted and flagged. Tags and entities are **not** interpreted or removed.
- Overlap/out-of-order starts, including overlap with an earlier long-running cue.
- Manual review decision and note per cue.

A quiet flag list does not mean that captions are accessible, accurate, synchronized, or ready to deliver. Review with the actual video and intended audience. CueDesk does not edit, translate, repair, transcribe, burn in, or certify subtitles.

## Input and privacy limits

Basic comma-timestamp SRT only: numeric unique cue IDs, `HH:MM:SS,mmm --> HH:MM:SS,mmm` (also three-digit hours), positive duration and nonempty text. At most **2 MiB / 5,000 cues**. BOM and CRLF are supported. WebVTT, ASS, SRT positioning extensions and non-UTF-8 encodings are not supported.

Video is loaded through a local object URL, not uploaded. Browser codec support and your device's resources limit playback. No application-level video size cap is imposed. All review state stays in the current tab; no browser storage is used. Downloaded reports remain on your device after clearing the app.

Reports omit source filename, original cue IDs, and caption text. They still include cue positions/times, metrics, decisions and **your notes**. These can be private. Check before sharing. Local operation is not a guarantee against a compromised browser, device, or extension.

## Build and test

Node.js 20 or newer, npm, and a recent browser with `Intl.Segmenter` are required for development.

```sh
npm ci
npm test
npm run build
```

Browser checks use Playwright and a synthetic video fixture:

```sh
npx playwright install chromium
ffmpeg -y -f lavfi -i color=c=navy:s=640x360:r=24:d=12 -c:v libx264 -pix_fmt yuv420p /tmp/cuedesk-test-video.mp4
npm run test:browser
```

Set `CHROME_PATH` to use an installed Chromium executable. Set `TEST_VIDEO` to another suitable 12-second-or-longer MP4 fixture. Test outputs go to `/tmp`. The fixture contains a solid color, no personal media.

Verified on 23 November 2026: **23 core tests and 19 Chromium browser checks**, including local video seek/approximate stop, literal-safe markup, report gating/omission, 390px overflow, and no external runtime requests. Desktop and emulated mobile layouts were visually inspected. Not tested on physical phones, Safari, or Firefox. Local HTML opening on mobile depends on the file viewer/browser; desktop use is the supported starting point.

## Why this small tool exists

This is a focused manual cue-review desk, not a replacement for mature subtitle tools and not a claim of a new category. [CueLint](https://github.com/Ax1zz/cuelint) and [SRT Check](https://github.com/AresE87/srt-check) already offer local linting/checking workflows. Use a full subtitle editor for changes. See [RESEARCH.md](RESEARCH.md) for the source notes and tradeoffs.

## License

MIT. See [LICENSE](LICENSE) and [THIRD_PARTY.md](THIRD_PARTY.md).
