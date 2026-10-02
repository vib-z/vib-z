# THE NEXT 30 SECONDS: farhan-syah/motion-video-skill

**Library:** motion-video v1.4.1 (`/home/user/farhan-syah/motion-video-skill`, commit cf0e89e).
**Format:** vertical 1080×1920 (9:16), 30 fps, built to the DIRECTION.md §10 rules.

| Deliverable | Value |
|---|---|
| `final.mp4` | 1080×1920, 30/1 fps, 900 frames, **30.000 s**. H.264 High, yuv420p, BT.709, faststart. AAC-LC 192 kbps, 48 kHz stereo. **13.05 MB** |
| Loudness | **−14.1 LUFS** integrated, **−1.7 dBTP** true peak, LRA 2.3 LU (ebur128 on the delivered file) |
| `poster.jpg` | Frame at 17.55 s: "1,300" has landed on the storm-lit Earth and its label is in. I moved it off 16.5 s because the counter is still rolling at that frame (§10.9 allows ~16.5–17.3 s; 17.55 s is the first frame with the number, label and bolts all settled) |
| `contact.jpg` | 8 vertical tiles, one per scene (1.62, 5.70, 9.70, 14.20, 17.40, 21.70, 24.70, 29.95 s) |
| blackdetect | No black segments. S8 goes dark but is never pure black, per §10.8 |

Project source: `/home/user/work/farhan-motion-video/video/`, which holds `direction.md`, `video.json`, `scenes/01…08`, `shared/`, `assets/` and `out/` (renders, `audit.png`, `sheet.png`, stems). Tools live in `/home/user/work/farhan-motion-video/tools/`: `score.py`, `births.py`, `lottie_pulse.py` and `finalize.sh`.

## Workflow as the skill prescribes it (direct → build → render)

1. `doctor`: found SwiftShader software WebGL, libx264 and no GPU. I planned for that: light 3D, no bloom passes, 2 workers.
2. `init video`, then I filled in `direction.md` (`references/direction.md`, `concepts.md`, `styles.md`). It has facts with sources, three concepts, three palettes, the sonic concept, an energy arc and a beat table.
3. `font "Archivo"` (Fontsource), plus `lib gsap three lottie`.
4. `map` (Natural Earth) for the births map and the globe texture.
5. Build. Each scene went through `still` / `probe` / `check`, and I reviewed the still sheets with Read.
6. `render --draft`, run twice, then `audit` + `sheet`. I fixed the cues and the layout after each pass.
7. Full `render` (check clean: **0 errors, 48 warnings**), which also writes the stems, `audit.png` and `sheet.png`.
8. A size-capped delivery encode from the library master (audio stream copied, so the library's loudness pass is preserved), then poster, contact sheet and QA.

## Which library feature drives which scene

| Scene | Library features (repo paths) | Hand-built on top |
|---|---|---|
| S1 Hook 0–4 | `.m`/keyframe motion and easing tokens (`templates/base.css`); **Lottie** pulse rings via `__video.use(anim)` (`templates/motion.js`, `lib lottie`); `thud` lub/dub and `hit` (braam) on the "30" slam (`scripts/lib/sound-catalog.mjs`); `riser` scene transition into S2 (`video.json` `"in"`, `scripts/lib/arc.mjs`); `.vignette`; film grain | Countdown ring HUD (`shared/hud.js`), ember particle canvas, tick-dial ring, word-timed karaoke on the kinetic words |
| S2 Heart 4–8 | Icon kit `data-icon="heart"` (`templates/icons.js`, Lucide); `data-count` 0→35 with `ticker` SFX; **leader line** `svg.links path[data-from][data-to][data-draw]` to the "≈70 BPM" callout; `--in:pop`; `data-captions` karaoke | ECG oscilloscope canvas, heartbeat pump, push-into-heart zoom-through |
| S3 Blood 8–12 | **GSAP + MorphSVGPlugin** timeline via `__video.use(tl)` (cell→gold dot morph); `data-count` to 70,000,000; `slam` on "70"; `drop` **container cue** with `data-sfx-accents` (cell bursts); `pop` on the morph; `whoosh` transition | 2,400-cell, 3-depth particle stream (canvas sprites, perspective dolly) |
| S4 Births 12–16 | **`video.mjs map`** (`scripts/lib/map.mjs`, Natural Earth 50m) with **125 `--pin`s**, inlined with `data-inline`; **3 `pluck` container cues** (pentatonic, key-snapped via `data-sfx-pitch`, `data-sfx-accents`) | Births allocation (`tools/births.py`), ripple ordering by great-circle distance from Delhi, camera pull-back, 3-layer parallax (dot field / map / bokeh) |
| S5 Drop 16–20 | **three.js** + `three/addons` **EffectComposer + RGBShiftShader** (`lib three`); `__video.wait` for async setup; `boom` + `subdrop` (`data-sfx-layer="allow"`) on the drop; `glitch` on the RGB-split ghosts; `.stars` | Earth module (`shared/earth.js`): the library's Mercator map reprojected to an equirectangular texture, shaders, procedural clouds, 16-light flash uniform, 2D bolt overlay, white flash, shake, iris close |
| S6 Orbit 20–23 | three.js; `whoosh` transition, plus a `whoosh` bound to the zoom ring (camera move); `thud` on "900" | Pull-back with a 90° camera roll so the orbit stands tall in 9:16, Sun sprites, 3 star layers, orbit and trail overlay, iris open, whip |
| S7 Light 23–26 | three.js; `swoosh` transition; `shimmer` on the 224× landing | Beam laps with a precessing plane, occlusion test, fused ring, speed lines, white-out |
| S8 Payoff 26–30 | Kit `.m` stagger (`--in:left`, `--out:blur-out`) for the dashboard; icon kit; `data-captions`; Lottie final pulse; `success` chime on "count"; `thud` lub/dub at 29.55 / 29.70 | Loop rebuild: "MAKE THE NEXT [00:00] COUNT." mirrors frame 0's "IN THE NEXT [00:30] SECONDS", the light ring collapses into the last 0, and the progress arc refills on the final beat |
| All | Fontsource `font` (Archivo variable, wdth 62 for numbers); `check`, `still`, `probe`, `render --draft`, `render`, `audit`, `sheet`; `music` + ducking + loudness + stems (`scripts/lib/encode.mjs`); `energy` curves, `sound.key: "D minor"`, `sound.space: "room"` | Tally rail of 6 live counters; word timeline (`out/voice/words.json` from `vo_timeline.json`) |

**Native vs hand-built, honestly:** the library supplied the pipeline, the seek runtime, typography loading, icons, maps, captions, counters, leader lines, CSS motion and every sound effect. It does **not** ship particles, a globe, camera rigs, post-FX or visual transitions. Every scene's hero visual is my own canvas or three.js code running on its `__video.on` hooks. The hooks are what make that easy and deterministic. I'd estimate the code is about 35% library and 65% hand-built.

**Capability checklist:**
- **Kinetic type synced to words:** S1 and S8 karaoke kinetic lines, plus library karaoke captions everywhere else.
- **Rolling counters:** 6, all landing on their word frames. I checked each one with frame grabs at ±2 frames of every hit: 1.26, 4.95, 8.86, 9.26, 12.38, 17.19, 20.87, 24.03, 28.81, 29.11.
- **Particles ≥1,000:** 2,400 cells (S3), plus 3,600 stars (S6).
- **A camera move in every scene.**
- **≥3-layer parallax:** S3, S4 and S6.
- **3D:** the three.js Earth.
- **Varied easing:** spring, expo, overshoot and ease-in slams.
- **Smear frames:** the 30/70/125 slams, the whip and the beam trails.
- **8 transition kinds:** match cut on the ring, zoom-through, morph, white flash plus glitch/RGB split, iris, whip/smear, hard cut to dark, and the ring collapsing into the 0 for the loop.
- **Post-FX:** glow, grain, vignette, chromatic aberration and shake.

## Sound

**SFX: all from the library's motion-synthesized catalog** (no samples, no `data-sfx-src`). There are 23 cues:
- `thud` ×4
- `hit`, `riser`, `ticker`, `whoosh` ×3, `slam`, `drop` (container), `pop`
- `pluck` ×3 (containers)
- `boom`, `subdrop`, `glitch`, `swoosh`, `shimmer`, `success`

The renderer measures each element's motion and places the sound on its frame. Transient sounds are pitched by on-screen size and snapped to the D-minor pentatonic scale.

**Music:** "music only when the user supplies it", so I composed an original score in code (`tools/score.py`: numpy/scipy synthesis, 120 BPM, D minor) and passed it in as `music.file`. It follows the §5 cue sheet:
- 0–4: drone and soft heart thumps
- 4.0: kick enters as lub-dub
- 8–12: four-on-the-floor, 8th hats, bass pulse
- 12–16: warm Bb–F–C–Dm chords and bells; riser and accelerating snare roll from 14.0; hard 8th-note gap at 15.75
- 16.0: drop (big kick, sub, crash, claps, growl bass, pumping supersaw, zaps)
- 20–23: wide Dm9 pad
- 23–26: 16th hats, arpeggio, reverse cymbal cut hard at 26.000
- 26–28: silence with faint room tone
- 28–30: swell

**Mix: the library's mixer** (`encode.mjs`). It ducks music hard under the voice and effects gently, normalizes with one linear gain to −14 LUFS, and applies a 4× oversampled limiter. Measured on its stems, **the voice sits 8.7–10.9 dB over the music** on lines L1–L7. L8 plays over silence, and L9's swell sits about 20 dB under the voice.

**Library `audit` on the final:** 19/23 cues in sync, 4 FAIL, 5 "masked by narration", and 1 arc failure ("hard edge" at frame 0).
- The hard edge is deliberate: §10.10 asks for a strong heartbeat transient on frame 0.
- The 4 FAILs are the GSAP-driven morph `pop`, two `pluck` containers whose children are 9-px map pins, and a `shimmer` whose box overlaps the "224" entrance. Frame grabs show these sounds landing on their visual events. These are audit-heuristic misses, but the library records them as failures.
- **I could not listen to the mix** (no audio playback in this environment). The judgement rests on stems, ebur128 and the audit.

## Problems hit and workarounds

1. **The mixer hard-codes a 1 s fade-in and a 2 s fade-out on supplied music** (`encode.mjs`: `afade=t=in:d=1`, `afade=t=out:st=total-2`). That would erase the 0.0 s heartbeat and the 28–30 s swell.
   - The heartbeats became library `thud` cues bound to the pulse ring.
   - The swell is pre-emphasized in the score by the inverse of the fade (capped).
   - `sound.fadeOut: 0` and `fadeIn: 0.02` keep the frame-0 transient and the end beat.
2. **Slow iteration.**
   - `check` steps through every scene at 15 fps for text, contrast and collision, which took 3–12 min here with 5 agents on 4 CPUs.
   - `render` re-runs it after *any* project file change, the score WAV included.
   - Drafts took 18 and 26 min, and the final took **27 min 50 s**. Capture runs on software WebGL (SwiftShader); the three.js scenes are the slow part.
3. **Linter and runtime friction.**
   - The kit's own `.vignette` is flagged as "covering" every text. I added `data-overlap-ok`.
   - Giant condensed numbers produced em-box "text collides" false positives. I set `line-height` to 0.74 and nudged the labels.
   - The kit's `.line` (line mask) and `.num` classes collided with my class names and silently broke the layout. I renamed mine.
   - GSAP-driven motion is invisible to SFX measurement, which only reads CSS/WAAPI animations, so I used manual `data-sfx-at`.
   - A CSS `steps()` keyframe that hid the countdown digits worked in `still` but not in `render`. I moved it into the JS hook.
   - The four-note `sting` (1.5 s) would be cut by the video end (audit fail), so "count" uses the two-note `success` chime instead.
4. **Narration and captions.**
   - `transcribe` would install about 500 MB of Whisper runtime. The brief already gives word times, so I wrote `out/voice/words.json` straight from `vo_timeline.json`, merging "1" + ",300" into "1,300".
   - Captions are the library's `data-captions` (≥70 px, stroke, active-word pill, ≤3 words), placed inside x 90–950 and y 250–1480.

**Render time:**
- Final render 27 m 50 s (check ≈ 6 min, capture and mux the rest).
- Delivery encode, poster and contact sheet: 1 m 42 s.
- Two drafts: 18 m and 26 m.
- All on a 4-CPU machine shared by 5 agents (load average 15–26).
- Disk footprint: about 0.5 GB.

## Scorecard (1–10, honest)

| Area | Score | Why |
|---|---|---|
| Motion | **7** | The CSS motion system, counters, leader lines, map inlining and GSAP/Lottie/three.js on one seek clock are solid and frame-exact. Every hero visual (particles, globe, orbit, light ring) was still hand-written. |
| Transitions | **5** | No visual transition vocabulary beyond the cloud-pass. Sound transitions (`in`) are built in. All 8 visual transitions were hand-built. |
| Sound | **8** | Motion-measured, key-aware, size-pitched synthesized SFX that land on their frames, plus energy curves, ducking, an exact −14 LUFS and stems. Weak spots: the hard-coded music fades, effects get masked under the voice, and the 1.5 s `sting` can't end a video. |
| Ease of use | **6** | Excellent docs and one CLI, but long feedback loops (a full check before every render), kit class-name collisions and linter false positives. |
| Agent-friendliness | **8** | Opinionated written guidance, a linter that prints fixes, plus `still`, `probe`, `audit.png` and stems. Everything is deterministic and file-based. It is slow on a CPU-only box. |

## Credits and licenses

- **Fonts:**
  - Archivo by Omnibus-Type (SIL OFL 1.1, via Fontsource `@fontsource-variable/archivo`)
  - JetBrains Mono and Inter (SIL OFL 1.1, bundled with the skill)
- **Icons:** Lucide (ISC), bundled `icons.js`.
- **Map data:** Natural Earth (public domain) via world-atlas, d3-geo and topojson-client (ISC).
- **Libraries:** three.js (MIT), GSAP incl. MorphSVGPlugin (GSAP standard no-charge license), lottie-web (MIT), Playwright (Apache 2.0).
- **Voice:** `_shared/vo/vo_full.wav`, Kokoro-82M `af_heart` (Apache 2.0), supplied by the brief and used as-is.
- **Self-generated:** the score (`tools/score.py`), all SFX (the library's synthesized recipes), the Lottie pulse JSON (`tools/lottie_pulse.py`) and all visuals.
- **Facts:** DIRECTION.md §7. Births distribution: approximate national shares (UN WPP 2024). Lightning hotspots: NASA LIS/OTD climatology.
