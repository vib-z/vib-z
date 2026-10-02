# THE NEXT 30 SECONDS — HyperFrames build

**Library:** [heygen-com/hyperframes](https://github.com/heygen-com/hyperframes) — CLI `hyperframes@0.8.111` (npm), registry from `main`, `@hyperframes/shader-transitions@0.8.112`, repo clone at `f16e509`.
**Deliverable:** `final.mp4` — 1080×1920 (9:16), 30 fps, 900 frames, 30.000 s, H.264 High yuv420p, `+faststart`, AAC-LC 192 kb/s 48 kHz stereo, 13.2 MB.
**Loudness (delivered file, ffmpeg `ebur128=peak=true`):** −14.1 LUFS integrated, true peak −1.5 dBTP, LRA 2.4 LU.
**Stills:** `poster.jpg` = 17.3 s (LIGHTNING / 1,300 just landed — chosen as the platform cover per §10.9, because at exactly 16.5 s the counter is mid-roll); `poster_16.5s.jpg` = the literal 16.5 s frame. `contact.jpg` = one vertical tile per scene (S1 2.0 s … S8 28.9 s).
**Source:** `/home/user/work/hyperframes/next30/` (composition: `index.html`, `src/*.js|css`, `audio/score.py`), `/home/user/work/hyperframes/tools/` (probe, QA sheets, `finalize.py`).

---

## 1. Workflow (skills followed as if installed — `hyperframes init` actually installed them)

| Step | Skill / doc (repo path) | What it drove |
|---|---|---|
| Route | `skills/hyperframes/SKILL.md`, `references/routes/general-video.md`, `references/brief-format.md` | narrated multi-scene custom film → `/general-video`, `flow: automation`, `storyboard: no` |
| Scaffold | `skills/hyperframes-cli/SKILL.md` | `npx hyperframes init next30 --non-interactive --example=blank --skill=general-video` |
| Contract | `skills/hyperframes-core/SKILL.md` + references | one paused root GSAP timeline on `window.__timelines`, `class="clip"` scenes with `data-start/duration/track-index`, seek-safe code (no clocks, seeded RNG) |
| Look | `skills/hyperframes-creative/references/house-style.md`, `video-composition.md`, `typography.md` | dark editorial palette tinted to crimson; serif / condensed / mono voices; video-scale type; bg/mid/fg layers |
| Motion | `skills/hyperframes-animation/SKILL.md`, `transitions/overview.md`, `adapters/three.md`, `adapters/gsap*.md` | GSAP choreography, shader-vs-CSS transition choice, Three.js through `hf-seek` |
| Catalog | `skills/hyperframes-registry/SKILL.md` | `npx hyperframes catalog --json` (386 items) → `npx hyperframes add …` ×24 |
| Audio | `skills/hyperframes-audio/SKILL.md`, `references/attributes.md`, `fx-registry.md`, `scripts/carve.mjs` | `<audio>` tracks, `<hf-audio-group>` buses, `data-fx-chain`, dynamic voiceover **carve** |
| Media | `skills/media-use/SKILL.md`, `audio/assets/sfx/CREDITS.md` | bundled SFX are Pixabay-licensed (not CC0/CC-BY/OFL) → not used; everything synthesised |
| Gates | `hyperframes lint`, `hyperframes check` | lint 0 errors; **check passed** (0 errors; warnings are transition-time overlaps + the intentional RGB-split copies; 60/60 WCAG AA) |
| Render | `hyperframes render --quality delivery --workers 2 --no-page-side-compositing` | final picture + engine audio mix |

## 2. Native features used, and what was hand-built

| Where | Native HyperFrames | Hand-built on top |
|---|---|---|
| everywhere | paused root GSAP timeline, `data-*` clip timing, `three` adapter (`hf-seek`), CSS-animation adapter (grain), layout-audit attrs (`data-layout-ignore`) | per-frame "driver" (the camera-shake component's property-setter pattern) for countdown digits, draining conic ring, live tally |
| transitions | **`@hyperframes/shader-transitions` (HyperShader)** — `cinematic-zoom` 7.82 s (zoom-through into the heart), `cross-warp-morph` 11.8 s (cell → warm dot), `flash-through-white` 15.85 s (pure white frame at 16.0), `whip-pan` 22.85 s, CSS-fallback hard cut 25.985 s (dark at 26.0) | 4.0 s match cut on the circle (ring → heart at the same 490 px), 17.19 s RGB tear, 19.7 s glitch-out |
| S1 hook | grain-overlay, vignette, headline-slam shake, conic-progress-ring technique | frame 0 = big 00:30 + crimson pulse ring + "In the next / 30 SECONDS", karaoke headline (captions merged into the type), HUD snap at 2.42 s |
| S2 heart | number-wheel rolling digits | SVG ECG sweep, beating heart + ripples |
| S3 blood | three adapter | 3,200 instanced Evans–Fung red cells with Poiseuille flow + 1,800 plasma specks; MSAA + bloom + chromatic-aberration post pass |
| S4 babies | the world-map block's data path (world-atlas Natural Earth + d3-geo) | procedural dot-matrix Earth shader; 125 seeded birth pops on land, facing camera at their pop time |
| S5 lightning | camera-shake (helper copied verbatim), rgb-glitch-text technique, number-wheel | 1,300 seeded strike sprites, 8 cloud-lighting super-flashes, 2D branching bolts, CA spikes on the drop |
| S6 orbit | — | continuous pull-back from the storm close-up to the orbit (the Sun slides out from behind Earth), orbit line + motion trail |
| S7 light | — | 26 accelerating light rings that converge into one blinding ring, speed-line canvas, whiteout |
| S8 payoff | caption-highlight | tally rail → 6-number dashboard (rolls to the final values at 27.0), countdown returns to centre, last frame = frame 0 layout (00:00 → loops to 00:30) |
| captions | **caption-highlight** component logic (word pages, active-word crimson box) | re-laid out for the 9:16 safe zone (≤3–4 words, ≥64 px), one copy per scene, 1-frame pre-roll |
| audio | `<audio>` framework playback, `<hf-audio-group>` buses (`voiceover`: highpass → compressor → presence peak; `sfx`: low-cut), `data-volume`, **`carve.mjs`** (strength 0.55: 4 peaking dips + level envelope, 7 automation lanes on the bed) | whole score + SFX synthesised in numpy (`audio/score.py`); final −14 LUFS / true-peak stage in ffmpeg |

**Registry items installed with `hyperframes add` (24):** blocks `flash-through-white, cinematic-zoom, whip-pan, glitch, sdf-iris, chromatic-radial-split, world-map, spiral-galaxy`; components `grain-overlay, vignette, camera-shake, caption-highlight, caption-pill-karaoke, caption-kinetic-slam, count-up, number-wheel, conic-progress-ring, motion-blur, rgb-glitch-text, match-cut, iris-reveal, headline-slam, beat-accent, chromatic-aberration-wipe`.
**Actually in the film:** 4 shader transitions (through the package those blocks demo; `cross-warp-morph` by name), grain-overlay, vignette, camera-shake, caption-highlight, number-wheel, rgb-glitch-text, conic-progress-ring, headline-slam, match-cut (technique), world-map (data path). Installed but **not** used: glitch / sdf-iris / chromatic-radial-split shaders, spiral-galaxy, count-up, iris-reveal, beat-accent, caption-pill-karaoke, caption-kinetic-slam, chromatic-aberration-wipe, motion-blur (removed, §4). Components are paste-in snippets by design; most were adapted (sizes, vertical layout, per-scene copies), not used verbatim.

**Checklist:** kinetic type on the word times; rolling counters; particles (3,200 cells + 1,800 specks, 1,300 strikes, 4,600 stars); a camera move in every scene; ≥3-layer parallax (ghost type/ring/type; wall/far/near cells; stars/Earth/overlays); 3D Earth ×3 + Sun; varied easing (expo, back, power4, sine); smear via cinematic-zoom + whip-pan shaders; bloom, grain, vignette, chromatic aberration + screen shake on the drop. Transition kinds: match cut, zoom-through, morph, white flash, whip pan, glitch/RGB split, hard cut to dark — 7 (no iris). §10: vertical, text inside x 90–950 / y 250–1480, frame 0 bright and moving, every VO word captioned karaoke-style, a pattern interrupt every ≤2 s, numbers 300–500 px tall when they land, S8 dark but keeps ring + captions, last frame matches frame 0.

## 3. Sound (original, all code)

`audio/score.py` (numpy/scipy, seeded) writes two stems. **Music** (A minor, 120 BPM): heartbeat lub-dub at 0.0/0.3 + drone → kick at 4.0 doubling as the heartbeat → hats + 8th bass at 8.0 → warm pads, riser and accelerating snare roll 14.0–15.75 with a hard 1/8-beat gap at 15.75 → **drop at 16.0** (kick, clap, 16th bass, stabs) → wide half-time pad at 20.0 → 16th hats + arpeggio at 23.0 → **sample-accurate silence at 26.0** (reverb tails gated) → chord swell from 28.0 → FM-bell sting on "count" 29.11 → heartbeat at 29.70. **SFX:** impacts on every number hit, whooshes, a zoom suck into 8.0, 125 pentatonic plinks timed to the birth pops, thunder + sub drop at 16.0, zaps on strikes, Doppler whoosh on the pull-back, 26 light "zips", reverse cymbal into 26.0, second ticks, faint room tone in the silence. HyperFrames mixes them (buses + carve). VO sits about 9–10 dB above the bed while speaking (measured from per-stem audio-only renders). Measured on the master: 26.02–26.24 s is −63 dB (room tone only), and the 15.75 gap is −95 dB.

## 4. What broke and the workarounds (honest)

1. **The sandbox Chrome could not load CDN scripts** (TLS through the proxy CA), so `check` reported `gsap is not defined`. Fix: vendored GSAP, three.js, d3-geo, topojson and the shader package.
2. **Shader transitions silently turned into hard cuts.** The producer only looks for `HyperShader.init(` in *inline* scripts (`packages/producer/src/services/htmlCompiler.ts → detectShaderTransitionUsage`). Mine was in `src/main.js`, so the log said `hasShaderTransitions:false`, with no warning. Fix: moved the init inline.
3. **WebGL scenes went blank inside transitions** with the default page-side compositor. It `cloneNode()`s the scenes (`packages/shader-transitions/src/engineModePageComposite.ts`), and a cloned `<canvas>` has no pixels. Fix: `--no-page-side-compositing` (Node-side layered blend, about 2× slower).
4. **The layered blend drops everything outside the two scenes** (`captureHdrFrameShared.ts`), so the HUD, captions and grain vanished during every transition. Fix: built HUD, tally, captions, grain and vignette **inside every scene**, all driven by the same timeline.
5. **The grain-overlay component froze the page.** Its 200%-size SVG `feTurbulence` layer, times 6 scenes, starved software-GL Chrome: `new WebGLRenderer()` never returned, DOMContentLoaded never fired, and each DOM frame cost about 7 s. Fix: a seeded PNG tile at 1× size, keeping the component's keyframe idea.
6. **motion-blur component + HyperShader** kept the main thread busy for about 40 s at load (its sub-frame re-seeks also run the shader timeline). Removed it.
7. **`check` first failed with `sweep_static`.** The harness ran my scripts before the scene markup existed (`null.appendChild`), so no timeline was registered. Fix: deferred the build until `#sc1` exists. `check` now passes.
8. **Render cost on 4 shared vCPUs with SwiftShader:** lathed instanced cells took about 15 s/frame. Instanced shaded quads take about 0.35 s/frame. The other agents pushed load average to 20–28 during the build.
9. **camera-shake** profiles add 3D rotation that throws a 9:16 frame off-screen at drop intensity. Fix: `rotation:false` and low intensity.
10. Repeated GSAP `fromTo` immediate-render collisions (frame 0 showed late-scene states). Fix: `defaults:{immediateRender:false}`. One of my own CSS edits also silently dropped rules; loop-frame QA caught it before the final render.
11. **No offline music/SFX source, bundled SFX not CC0/CC-BY, and no master-bus loudness target or true-peak limiter.** Fix: synthesised everything, then added `tools/finalize.py`. It applies measured gain plus a 4×-oversampled limiter, checks the result on the *encoded AAC*, trims the AAC to 29.97 s so the container is exactly 30.000 s, and runs a 2-pass x264 encode to fit 14 MB. The limiter needed about 4–5 dB of peak reduction to reach −14 LUFS.
12. `doctor` wanted to download its own Chrome. Fix: pointed `HYPERFRAMES_BROWSER_PATH` at the preinstalled `/opt/pw-browsers/chromium_headless_shell-1194`. The engine still fell back to screenshot capture: no BeginFrame on the layered path, and software GL.

Residual flaws: rolling digits show neighbouring numerals while they spin. The storm Earth reads a little hazy rather than crisp. The orbit Sun is close to blown out. No iris transition.

## 5. Render time

Final picture: **24 m 22 s** for `render --quality delivery --workers 2 --no-page-side-compositing` (900 frames, layered composite, software GL). Earlier full drafts took 15 m 44 s (shaders undetected) and 27 m 28 s (with shaders, under heavy machine load). Audio-only check renders (`--composition audiocheck.html`, blank picture) took about 45 s each. The delivery pass (loudness + 2-pass x264) took about 1 min.

## 6. Scorecard (1–10, scoring the library)

| | Score | Why |
|---|---|---|
| Motion | **8** | GSAP and Three.js adapters are solid and truly seek-deterministic. Registry primitives (number-wheel, camera-shake, caption logic) are well engineered. Particles and 3D are fully DIY. |
| Transitions | **7** | The shader set looks professional (zoom, morph, white flash, whip). But the flagship feature has three silent traps: inline-only detection, blank WebGL in page-side capture, and the layered path dropping overlays. |
| Sound | **6** | Strong native mixing: buses, fx chains, and a one-command dynamic voiceover carve that works. Missing: an offline music/SFX source (bundled SFX are Pixabay-licensed) and any master loudness or true-peak stage. |
| Ease of use | **5** | Great CLI and docs, but too many silent failure modes on a heavy composition with software GL: a registry component froze the page, canvases rendered blank, transitions fell back to hard cuts, and the working path is slow. |
| Agent-friendliness | **8** | Excellent skill set, `catalog --query/--json`, a non-interactive CLI, and `lint`/`check`/layout attributes written for agents. Every trap above was diagnosable from readable source. |

## 7. Asset credits

- Narration: provided `_shared/vo/vo_full.wav` (Kokoro `af_heart`), unedited apart from bus EQ and compression.
- Music & SFX: original, synthesised in code (`audio/score.py`). No samples.
- Fonts (SIL OFL 1.1, files via Fontsource): League Gothic (The League of Moveable Type), Instrument Serif (Instrument), Montserrat (J. Ulanovsky et al.), JetBrains Mono (JetBrains).
- Land data: Natural Earth (public domain) via `world-atlas@2` (ISC, Mike Bostock), drawn with `d3-geo` and `topojson-client` (ISC).
- Libraries: HyperFrames, its registry and `@hyperframes/shader-transitions` (Apache-2.0); GSAP 3.14 (GreenSock standard no-charge license); three.js r181 (MIT).
- Grain tile, textures, starfields, and the Earth, Sun and cell shaders: generated in code.
- Numbers: DIRECTION.md §7 (70 bpm; ~2.4 M RBC/s; UN WPP ~4.2 births/s; NASA LIS/OTD ~44 flashes/s; 29.8 km/s; 299,792 km/s × 30 s ÷ 40,075 km).
