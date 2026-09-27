<div align="center">

<img src="docs/app-icon.png" width="120" alt="MyTV app icon" />

# MyTV for Mac

**A native macOS app for watching live TV — an IPTV player with on-device AI live-translation subtitles, running entirely offline on your own Mac.**

[![platform](https://img.shields.io/badge/platform-macOS%2026%2B-000000?logo=apple&logoColor=white)](#requirements)
[![arch](https://img.shields.io/badge/architecture-Apple%20Silicon-orange)](#requirements)
[![swift](https://img.shields.io/badge/Swift-SwiftUI%20%2B%20libmpv-F05138?logo=swift&logoColor=white)](#tech-stack)
[![license](https://img.shields.io/badge/license-personal%20use-blue)](LICENSE)
[![download](https://img.shields.io/github/v/release/kanekanefy/mytv-for-mac?label=download&color=2ea44f)](https://github.com/kanekanefy/mytv-for-mac/releases/latest)

[简体中文](README.md) ｜ **English** ｜ [日本語](README.ja.md)

[Features](#features) · [Screenshots](#screenshots) · [Install](#install) · [Getting started](#getting-started-add-a-playlist) · [FAQ](#faq) · [Privacy](#privacy) · [Roadmap](#roadmap)

</div>

---

## About this repo

This is a **distribution-only repository** for a personal project: it holds the installer, documentation and screenshots — **no source code**. If someone sent you a link to this repo, jump straight to [Install](#install).

Code pull requests aren't accepted (there's no app source in this repo to merge into). Small documentation/wording fixes are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). For help, check [SUPPORT.md](SUPPORT.md) first; for security reports, see [SECURITY.md](SECURITY.md).

## Features

| Category | Capability |
|---|---|
| Live sources | m3u / m3u8 / txt (tvbox-style) playlists, automatic merging of duplicate channels across multiple sources, built-in public playlist you can switch on with one click |
| EPG | Fetches and displays the current/next program with a progress bar |
| Playback | Hardware decoding via libmpv (VideoToolbox), automatic 1080i de-interlacing, lockable/auto-stretch aspect ratio |
| Channel logos | Automatically matched and displayed |
| On-device live-translation subtitles | Foreign-language broadcasts → Chinese subtitles, fully local inference — no network calls, no audio ever uploaded |
| Interpreter mode | Video is automatically delayed a few seconds so picture and subtitles line up; a transition animation smooths the delay in/out instead of a jarring jump |
| Bilingual subtitles | Original + translated text on screen together, two layout options |
| Per-channel auto language detection | No manual language picking — it figures out what language a channel is speaking |
| Model comparison / blind rating | Two translation models side by side on the same stream, with blind A/B voting to collect data |
| Foreign-language channels (optional) | A bundled list of public documentary/foreign channels from iptv-org, off by default, one toggle in Settings |

## Screenshots

<p align="center"><img src="docs/screenshots/live-interpretation-en2zh.jpg" alt="Live interpretation: English to Chinese" width="100%" /><br/><sub>Live interpretation (EN → ZH): on-device model translation, subtitles synced to speech, "live interpretation" indicator top-right</sub></p>

<table>
<tr>
<td width="50%"><img src="docs/screenshots/bilingual-stacked.jpg" alt="Bilingual stacked" /><br/><sub>Bilingual stacked (ZH → EN): translation as the primary line, original as a secondary line</sub></td>
<td width="50%"><img src="docs/screenshots/bilingual-top.jpg" alt="Bilingual, original on top" /><br/><sub>Bilingual, original on top: source text placed above the picture, automatically avoiding channel logos and burned-in subtitles</sub></td>
</tr>
<tr>
<td width="50%"><img src="docs/screenshots/compare-mode.jpg" alt="Model comparison" /><br/><sub>Model comparison: two translation models side by side, with optional blind voting</sub></td>
<td width="50%"><img src="docs/screenshots/channel-browser.jpg" alt="Channel browser" /><br/><sub>Channel browser: groups, logos, search, program guide</sub></td>
</tr>
<tr>
<td width="50%"><img src="docs/screenshots/settings-source.png" alt="Playlist settings" /><br/><sub>Playlist settings: built-in public sources, or add your own URL</sub></td>
<td width="50%"><img src="docs/screenshots/settings-translation.png" alt="Translation model library" /><br/><sub>Translation model library: recommended picks by language direction, one-click in-app download</sub></td>
</tr>
</table>

> Screenshots use the built-in public playlist (500+ channels from vbskycn); no private channel configuration is shown.

## Requirements

- macOS 26 or later
- Apple Silicon (M-series); Intel Macs are not supported
- ~100MB of disk space for the app itself; the live-translation feature downloads a model on first use (see below)

## Install

1. Download the latest `MyTV-for-Mac-x.x.x.dmg` from this repo's [Releases](../../releases) page
2. Open the DMG and drag "我的电视" (MyTV) into Applications
3. **The first launch will be blocked by macOS** — this build isn't notarized with a paid Apple Developer ID, so Gatekeeper doesn't recognize it yet. Use any one of the following to allow it:
   - **Right-click** the app → "Open" → click "Open" again in the confirmation dialog
   - Or: open **System Settings → Privacy & Security**, scroll down to the line that says "我的电视" was blocked, and click "Open Anyway"
   - If neither option appears, run this once in Terminal:
     ```bash
     xattr -dr com.apple.quarantine "/Applications/我的电视.app"
     ```
4. After that, just double-click to open normally — this is only needed once

A more detailed, step-by-step walkthrough (with a troubleshooting table) is in [docs/installation.md](docs/installation.md).

## Getting started: add a playlist

The app ships with a public IPTV playlist (500+ channels) enabled by default, so it's watchable **immediately with zero setup**.

If a friend gave you your own playlist URL: open MyTV → menu bar "我的电视" → "设置…" (Settings) → the "订阅源" (Sources) tab, paste the URL, and click "应用并刷新" (Apply & Refresh).

Want international documentary channels like BBC Earth or National Geographic? Settings → "订阅源" (Sources) → find the "国际纪实 / 外语台" (International / foreign-language) entry and toggle it on (off by default). These are public streams from [iptv-org](https://github.com/iptv-org/iptv).

## Using live-translation subtitles

1. While playing any channel, press `Y`, or use the menu bar "翻译" (Translation) → "开启实时翻译字幕"
2. **The first time, you'll be prompted to download a model** (the default tier is ~1.5GB — a purely local GGUF model, not a cloud API call). The model library is under Settings → "翻译" (Translation); pick one and download it. On networks in mainland China, the app prefers a ModelScope mirror for faster downloads
3. Once downloaded, the model loads automatically and subtitles appear within seconds; the source language is detected per channel automatically, or you can set it manually
4. Everything runs on-device (a bundled `llama-server` subprocess with Metal acceleration) — no network calls, no audio upload, no dependency on any cloud API

## FAQ

**Why does the first launch say "cannot be opened because the developer cannot be verified"?**
See step 3 under [Install](#install) above — right-click to open, or allow it once in System Settings. This is expected: an individual developer build without a paid Apple notarization.

**Live translation doesn't work / it says `llama-server` is missing?**
The local inference runtime is already bundled inside the app — nothing extra should need installing. If you do hit an error, please include the log file (Settings → Debug shows the path, normally `~/Library/Logs/MyTV/`) when reporting the issue.

**Does it secretly upload my data?**
No. Speech recognition, sentence segmentation and model inference all run on-device. The only network access is fetching whichever IPTV/EPG URL you configured, plus the one-time translation model download. See [Privacy](#privacy) below.

**Can it run on an Intel Mac / macOS 25 or earlier?**
No. It relies on APIs only available starting in macOS 26 (the system-level `SpeechAnalyzer` for speech recognition, among others), and only an Apple Silicon build is provided.

**Why does the icon/name look similar to an Android "XX TV" project?**
This is a from-scratch macOS-native rewrite in Swift + SwiftUI + libmpv. It's inspired, in scope and feature direction, by the Android open-source project [yaoxieyoulei/mytv-android](https://github.com/yaoxieyoulei/mytv-android) (MIT-licensed) — but the code is an independent implementation, not a port.

## Privacy

- **Translation runs entirely on-device**: speech recognition (system `SpeechAnalyzer`) and text translation (a local GGUF model, run through a `llama-server` subprocess) both happen fully offline — no audio upload, no subtitle text upload, no dependency on any cloud translation API (unless you manually configure a third-party OpenAI-compatible endpoint yourself in Settings)
- **No telemetry is sent to the author**: debug logs are written locally (path shown in Settings) and stay on your own machine
- The app itself doesn't ship with anyone's private IPTV playlist — you either bring your own or use the built-in public source

## Credits & third-party components

See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).

## Roadmap

- V2: split the translation pipeline into a standalone service so multiple devices/TVs can share one on-device inference backend (over LAN, or via Tailscale for remote setups)
- Exploring an Android TV build

## Tech stack

SwiftUI + AppKit (native macOS UI) · libmpv (playback core, VideoToolbox hardware decoding) · system `SpeechAnalyzer` (speech recognition) · llama.cpp / GGUF (on-device translation inference)

---

<div align="center">
<sub>Feedback: <a href="../../issues">Issues</a> (check <a href="SUPPORT.md">SUPPORT.md</a> first) · Security: <a href="SECURITY.md">SECURITY.md</a> · This is a distribution-only repository for a personal project — no code PRs, see <a href="CONTRIBUTING.md">CONTRIBUTING.md</a></sub>
</div>
