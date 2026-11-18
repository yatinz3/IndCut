# IndCut Studio

**A fully offline, CapCut-style video editor for Windows.** Built with Tauri (Rust) + a single-file HTML frontend — no cloud services, no external asset downloads. Every asset is embedded or generated on your machine.

Made by **yatinz3**. 🇮🇳

---

## ✨ Features

### Home / project manager
- **CapCut-style home screen** with Home, Templates, and Drafts sections
- **Multiple independent projects** — create, open, rename and delete drafts
- Projects auto-save locally (localStorage) as you work
- **Templates** that auto-configure the editor by name (e.g. Reel/Short → 9:16, Trailer → 2.39:1, Podcast → 1:1)
- **Made in India** badge
- **☕ Buy me a coffee** popup — UPI: `yatinz3@ptyes` (with copy button)
- **💬 Join Community** — opens the Discord invite directly (auto-join)

### Editor UI
- Horizontal top tabs like CapCut: Media, Audio, Text, Stickers, Elements, Effects, Overlays, Animate, Transitions, Adjust, Speed, Chroma, Captions, Templates, Brand
- **Resizable side panels** (Media and Project) and **resizable timeline** — drag the dividers
- **Collapsible library sections** — expand/contract every group
- **Ratio dropdown under the video preview** — 16:9, 9:16, 1:1, 4:5, 21:9, 2.39:1, 4:3, 3:4, 5:4, 2:1, 3:2, 9:16 Story
- Editable frame rate (24/30/60 fps), background colour — all auto-apply with no Save button
- **Preview on click** + **+ Apply button** on library cards
- UI customization: accent colour, font, brand kit (all auto-apply)

### Timeline
- 4 default tracks (Video, Overlay, Text, Audio) — **add as many extra track lines as you want**
- **Magnetic auto-arrange** — clips push each other so nothing overlaps
- **CapCut-style alignment guide** — red line when snapping to a cut, cyan for playhead
- Drag clips between any tracks, trim handles, split, duplicate, delete
- Playback controls under the preview: play/pause, previous/next frame, start/end, loop

### Libraries (all offline)
| Library | Count |
|---|---|
| Filters | 132 |
| Transitions (incl. censor wipes) | 87 |
| Stickers | 1238 |
| Animations (in / out / loop) | 103 |
| Audio sounds (procedurally generated) | 33 |
| Project templates | 25 |
| Backgrounds (procedural gradients) | 36 |
| Text templates | 55 |
| Elements, overlays, keyframe presets, speed curves (23) | — |

- **Effects, transitions and animations apply to the selected clip** (video, image or text)
- **Keyframes** with easing (ease, back, elastic, bounce) applied in the renderer
- **Speed curves** that actually change playback mapping
- **Chroma key** — screen / colour / luma modes with similarity and feather
- Live canvas previews for effects, transitions and animations

### Export
- CapCut-style export dialog: custom filename, resolution (480p–4K), fps, quality presets, format (MP4/WebM), estimated size and progress bar
- The `yatinz3` watermark is **hidden in source only** — never burned into exported videos

---

## 📦 Downloads

Prebuilt installers are in [`release/`](release/):
- `indcut_0.1.0_x64-setup.exe` (NSIS)
- `indcut_0.1.0_x64_en-US.msi`
- `IndCut-Studio.html` (single-file portable build — just open in a browser)

---

## 🔨 Building from source

```powershell
# 1. Build the single-file frontend
powershell -ExecutionPolicy Bypass -File studio/build-single.ps1

# 2. Build the desktop app (requires Rust + Node)
cd indcut-ui
$env:Path = "$env:USERPROFILE\.cargo\bin;" + $env:Path
npx tauri build
```

Installers land in `indcut-ui/src-tauri/target/release/bundle/`.

### Development server

```powershell
node studio/serve.js
# open http://127.0.0.1:8099/IndCut-Studio.html
```

---

## 📁 Project structure

```
studio/
  app.js               # all app logic, libraries, renderer, project manager
  app.css              # CapCut-style UI theme
  index.template.html  # UI layout / home screen / modals
  build-single.ps1     # bundles into one HTML file (UTF-8 safe)
  serve.js             # local dev server
indcut-ui/             # Tauri desktop wrapper (Rust backend)
IndCut-Studio.html     # built single-file app
release/               # staged installers for distribution
PUBLISH.md             # GitHub release instructions
```

---

## 🤝 Contributing

Join the Discord community (button on the home screen) to share ideas, suggest features and contribute.

## 📄 License

See [LICENSE](LICENSE).
