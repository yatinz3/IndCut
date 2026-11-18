# IndCut Studio

**A fully offline, CapCut-style video editor for Windows.** Built with Tauri (Rust) + a single-file HTML frontend — no cloud services, no external asset downloads. Every asset is embedded or generated on your machine.

Made by **yatinz3**. 🇮🇳

---

## ✨ What's included

### Home & project manager
- CapCut-style home screen with **Home** and **Drafts** sections
- Multiple independent projects — create, open, rename, delete
- **Auto-save**: every 1 minute, on change (debounced), and on close — media persisted in IndexedDB, isolated per project
- Templates that auto-configure the editor by name (Reel/Short → 9:16, Trailer → 2.39:1, Podcast → 1:1)
- **Appearance selector on the home screen** — Dark / Light / System (saved locally)
- **Made in India** badge (bottom-center) and **"by yatinz3"** in white
- **☕ Buy me a coffee** — UPI `yatinz3@ptyes` (copy button)
- **💬 Discord** — `discord.gg/yghw6WaAqt`
- **▶ YouTube** — `@yatinz`

### Editor UI (custom layout)
- **Scrollable left vertical tab rail** with 15 tabs: Media, Audio, Text, Stickers, Elements, Effects, Overlays, Animate, Transitions, Adjust, Speed, Chroma, Captions, Templates, Brand
- Compact bars, **centered play/pause**, **time display on the right**, **ratio dropdown in the transport bar**
- **Dashed alignment guides**, clean panels, no unnecessary info sections
- Resizable side panels and timeline; collapsible library sections
- Ratio options: 16:9, 9:16, 1:1, 4:5, 21:9, 2.39:1, 4:3, 3:4, 5:4, 2:1, 3:2, 9:16 Story
- Frame rate (24/30/60) and background colour auto-apply — no Save button
- **Live hover previews** on library cards + "+" apply button

### Timeline & editing
- 4 default tracks (Video, Overlay, Text, Audio) — add unlimited extra tracks
- Magnetic auto-arrange; red/cyan alignment guides; drag, trim, split, duplicate, delete
- **Right-click context menus** for clips and imported media
- Canvas overlay editing: dashed selection box, move/resize/rotate handles, box follows keyframes and playback
- **Transition box** centered on the clip joint, 40% opaque, with duration handle, inspector and edge guides
- **Keyframes**: per-property, diamond adds all transform properties, linear easing, interpolation for text x/y/scale/rot/opacity, live panel updates while dragging

### Text
- Content group at top with font dropdown — **44 font families**
- Colour / Style / Animation groups; size handled by Transform scale (0–300)
- Many named in/out/loop text animations (fade, slide, zoom, rotate, bounce, blur, typewriter, glitch, neon, etc.)

### Audio
- Per-clip volume slider with +/- and presets, fade in/out, normalize
- **Separate audio** from clips
- **Mic button** records voice-over to an audio track

### Effects & transitions
- Effects added as **fx clips** on the Effects track (default 2s)
- Transitions added to the best/selected clip at joints, default 0.4s, with a centered 40%-opaque box and inspector (Type / Duration / Remove)

### Other tools
- **Speed curves** (23) that actually change playback mapping
- **Chroma key** — screen / colour / luma modes with similarity and feather
- Adjust, Captions, Templates, Brand kit panels

### Export
- CapCut-style dialog: filename, resolution (480p–4K), fps, quality presets, format (MP4/WebM), size estimate, progress bar
- The `yatinz3` watermark is **visible during playback** but **never burned into exported videos** (stated in the dialog)

---

## 📚 Libraries (all offline — 5,100 items)

Counts measured from the shipped build:

| Library | Count |
|---|---|
| Filters | 3,487 |
| Transitions | 87 |
| Stickers | 1,238 |
| Overlays | 54 |
| Elements | 36 |
| Animations (in / out / loop) | 49 / 30 / 24 |
| Audio sounds (generated on this machine) | 33 |
| Project templates | 25 |
| Backgrounds (procedural gradients) | 36 |
| Text templates | 62 |
| Text animations | 33 |
| Speed curves | 23 |

Everything is generated on the machine (emoji, SVG, CSS gradients, canvas, Web Audio) or embedded as data URLs — **no runtime network calls**.

---

## 📦 Downloads

Prebuilt builds are in [`release/`](release/):
- `indcut_0.1.0_x64-setup.exe` — NSIS installer, Windows x64 (**latest**, rebuilt with the current UI)
- `IndCut-v0.1.0-arm64.apk` — Android ARM64 (needs JNI fix — see Future goals)
- `IndCut-Studio.html` — single-file portable build (open in a browser)
- `screenshot.png`

---

## 🔨 Building from source

```powershell
# 1. Build the single-file frontend
powershell -ExecutionPolicy Bypass -File studio/build-single.ps1

# 2. Copy the built HTML into the Tauri frontend dist
#    (indcut-ui/dist/index.html must match IndCut-Studio.html)

# 3. Build the desktop app (requires Rust + Node)
cd indcut-ui
$env:Path = "$env:USERPROFILE\.cargo\bin;" + $env:Path
npx tauri build
```

Installers land in `indcut-ui/src-tauri/target/release/bundle/nsis/`.

### Development server
```powershell
node studio/serve.js
# open http://127.0.0.1:8099/IndCut-Studio.html
```

---

## ✅ Current status

- **Health check passed**: 5,100 items, all 15 tabs, 0 console errors
- Verified: new project, background → preview, hover demos, adding effects, export modal
- **Final installer rebuilt** with the current web build (the previous exe was stale)
- **App binary launches** without crashing (window titled "indcut")
- The user-provided **logo was never changed** — it remains the source of truth
- Test servers and test files were removed; only the main app and final build remain

---

## 📁 Project structure

```
studio/
  app.js               # app logic, libraries, renderer, project manager
  app.css              # CapCut-style UI theme
  index.template.html  # layout / home screen / modals
  build-single.ps1     # bundles into one HTML file (UTF-8 safe)
  serve.js             # local dev server
indcut-ui/             # Tauri desktop wrapper (Rust backend)
  dist/index.html      # frontend served by the desktop app
  src-tauri/           # Rust entry, commands, icons, NSIS config
IndCut-Studio.html     # built single-file app
release/               # staged installers for distribution
PUBLISH.md             # GitHub release instructions
```

---

## 🔮 Future goals

- **Official trusted-source library** — port harvested open-source catalogs (gl-transitions, LUTs, LYGIA, animate.css/framer-motion, Tabler/Lucide, Noto/OpenMoji/Twemoji, Google Fonts, Tone.js) into the main app with an attribution screen, using only distribution-compatible licenses
- **Compact everything into one download** — embed the whole library into a single self-contained app so one file includes everything, fully offline
- **Free/open-source software** — keep evaluating compatible sources for future features; avoid non-commercial or ShareAlike assets
- **Platform** — revisit the Android APK JNI issue; consider Microsoft Store later for SmartScreen (no code-signing certificate yet); keep the logo/branding unchanged

---

## 🤝 Contributing

Join the Discord community (button on the home screen) to share ideas, suggest features and contribute.

## 📄 License

See [LICENSE](LICENSE).
