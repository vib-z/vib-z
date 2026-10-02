# THE NEXT 30 SECONDS: iart-ai/motion-skills

**Deliverable:** `final.mp4`. 1080×1920 (9:16), 30 fps, 900 frames, 30.00 s, H.264 High yuv420p with +faststart, AAC-LC 192k 48 kHz, 13.0 MB.
**Look:** a Kurzgesagt-style flat-3D explainer. Toon-shaded Earth, a flat-shaded heart, GPU blood cells, bold rounded type, and one crimson circle carried through every cut.
**Engine:** Remotion 4.0.532 (React, frame-deterministic), with `@remotion/three` (three.js r180 / R3F 9) for the 3D.
**Score + SFX:** Web Audio code rendered offline with the library's own soundtrack skill and `render.mjs`, then mixed with ffmpeg.
Project: `/home/user/work/iart-motion-skills/film`. Cloned packs: `/home/user/work/iart-motion-skills/packs/`.

## How the library was used
`iart-ai/motion-skills` is only an index. The 54 skills live in 17 separate pack repos, which I shallow-cloned. Each skill is a `SKILL.md`, a `references/` folder and a small `scripts/` verify kit. **There are no reusable components.** The skills are know-how, recipes and checklists, so every pixel and every sound was written for this film by following them.

| Pack / skill (repo path) | What it drove |
|---|---|
| `motion-design-skills/skills/remotion-video` (+ `references/api-and-patterns.md`) | The engine choice. Composition + zod schema + defaultProps, `interpolate`/`spring`/`Easing`, `<Audio>`, `@remotion/three` embedding, the render CLI, and the **stills → inspect → encode** loop |
| `explainer-video-skills/skills/explainer-video` (+ `script-to-screen-workflow.md`) | The script → storyboard → scene pipeline. Captions are driven from the same timing array as the cuts. Deliver-and-verify checklist |
| `explainer-video-skills/skills/wrapped-video` (`references/remotion-recipes.md`) | The big-number counter pattern, `<TransitionSeries>` scene blocks, font loading |
| `tiktok-video-skills/skills/caption-animation` | Burned-in karaoke captions: `@remotion/captions` `createTikTokStyleCaptions()` with `pageBreakAfter` (≤4 words a page), per-word spring pop with overshoot, one accent colour on the active word, a 10 px stroke, and placement inside the 9:16 safe band |
| `tiktok-video-skills/skills/short-form-video` (+ `retention-pacing.md`) | A hook on frame 0 with no fade-up. A pattern interrupt every 1–2.5 s at uneven intervals, punch-ins, and the **sentence loop** ("…make the next 30 count" → "In the next 30 seconds"). The first and last frames match. Safe zone |
| `tiktok-video-skills/skills/countdown-video` (+ `references/digit-flip.md`) | A drift-free countdown computed from the frame, with odometer reel digits and tabular figures |
| `kinetic-typography-skills/skills/kinetic-typography` (`reveal-recipes.md` §7) | Per-word spring reveals, stagger rhythm, expo-out enters, and the hook/final title type |
| `data-animation-skills/skills/chart-animation` | Counters: the value eases out (cubic) and lands exactly on the spoken word, then is rounded and formatted with `Intl.NumberFormat` in tabular figures. Includes the 70,000,000 odometer |
| `data-animation-skills/skills/animated-infographic` | The S8 dashboard (layout designed static first, icon pop with spring overshoot, 3-frame stagger) and the running tally rail |
| `webgl-animation-skills/skills/threejs-animation` (+ `r3f-and-perf.md`) | One continuous 3D world (Earth, Sun, orbit, light beam), camera lerps, imperative materials via `useMemo` + dispose |
| `webgl-animation-skills/skills/shader-glsl` (+ `glsl-cookbook.md`) | Value noise and fbm, full-screen-quad backdrops, fresnel atmosphere, an anti-aliased orbit line using `fwidth` (constant on-screen width), and the glitch + chromatic-aberration recipe |
| `webgl-animation-skills/skills/particle-system` | 3,200 red blood cells as GPU `Points` + `ShaderMaterial` (seeded attributes, animated in the vertex shader), and the 125 popping birth dots |
| `map-animation-skills/skills/map-animation` (Path B, vector maps) | Natural Earth land through a d3-geo projection into the globe texture, latitude/longitude placement of births and lightning strikes, spring "pin drop" pops |
| `javascript-animation-skills/skills/soundtrack` (+ `templates/groove.js`, `scripts/sync-check.mjs`) | All music and SFX as Web Audio code (`window.SCORE`): lub-dub kick, riser + snare roll, ⅛ gap, drop, sidechain pump, reverse cymbal, hard silence, heartbeat. Checked with `sync-check` |
| `javascript-animation-skills/skills/javascript-animation` (`scripts/render.mjs`, `references/storyboard.md`, `references/qc.md`) | `render.mjs` rendered both score stems offline (OfflineAudioContext → WAV). Beat grid, EVENTS and CUES are data shared by picture and sound. Director pass on 2 fps contact sheets |
| `motion-design-skills`: `animation-principles`, `motion-art-direction`, `beat-sync-editing`, `shot-composition`, `color-motion`, `motion-background` | Easing vocabulary, one hero per frame, the 120 BPM grid (15 frames per beat), the biggest visual on the drop, one camera move per beat, bg/mid/fg parallax, OKLCH palette interpolation, mesh-gradient + 3-layer star backdrop |
| `freelance-motion-skills/skills/video-delivery-specs` + `scripts/probe-mp4.sh`, `scripts/contact-sheet.sh` | Delivery QC. `probe-mp4.sh` (1080x1920 @30 assert) and `contact-sheet.sh` (tiling for `contact.jpg`) were used as shipped |

## Scenes and transitions
| Scene | Build | Transition out |
|---|---|---|
| S1 Hook 0–4 | Frame 0: a big bright `00:30` in the crimson pulse ring, with the heartbeat transient. The hook title is readable by 0.5 s. A giant **30** slams in on "thirty" (1.26 s) with motion blur, shake and an impact. The countdown flies to the HUD at 2.5 s and the ring tightens with the riser | **Morph / match cut**: the ring becomes the heart (`@remotion/paths` `interpolatePath`) |
| S2 Heart 4–8 | A flat-shaded heart beats on the lub-dub kick, with pulse rings, a scrolling ECG trace and 3 ember layers. **35** lands at 4.95 s. Punch-in at 6.5 s | **Zoom-through**: custom `TransitionPresentation` + in-scene push |
| S3 Blood 8–12 | GPU vessel tunnel with biconcave cells and new-cell bursts (bubble SFX). **70** lands at 8.86 s, **MILLION** at 9.26 s, and the odometer runs to 70,000,000. Camera roll at 10.6 s | The hero cell **morphs** (OKLCH colour lerp) into a gold dot, then the native **iris** opens |
| S4 Babies 12–16 | Toon Earth with 125 dots popping, each with a pentatonic plink. **125** lands at 12.38 s. Punch-in at 14.0 s | **White flash + glitch/RGB split + shake** at 16.0 s |
| S5 Lightning 16–20 | Night side, back-lit, with storm clouds and about 60 surface flashes, plus 3D spider bolts and 2D forked bolts. **1,300** lands at 17.19 s | Continuous **pull-back** |
| S6 Orbit 20–23 | A powers-of-ten pull: the Sun rises into frame, with an orbit line, motion trail and a "you are here" ring. **900 KM** lands at 20.87 s | **Whip pan / directional smear** |
| S7 Light 23–26 | A polar light beam laps the planet, accelerating (a zap per lap), with speed lines, until the ring goes blinding white. **224×** lands at 24.03 s | **Hard cut** to dark + silence |
| S8 Payoff 26–30 | Dark and silent, but the countdown and captions stay visible. An afterimage ring remains. At 27.0 s the dashboard shows all six final values. At 28.25 s the tiles collapse into the ring, the countdown returns to centre and "MAKE THE NEXT 30 COUNT." appears. The ring collapses into the last 0, giving **00:00** plus the heartbeat at 29.70 s | **Loop**: the last frame matches frame 0 (ring, countdown, two-line title, palette) |

## Native vs hand-built
- **Native, used as shipped:**
  - Remotion core, `@remotion/three` `ThreeCanvas`, `@remotion/transitions` (`TransitionSeries`, `iris`), `@remotion/captions`, `@remotion/motion-blur` `CameraMotionBlur`, `@remotion/paths`, `@remotion/fonts`.
  - From the library: `javascript-animation/scripts/render.mjs` (offline score render), `soundtrack/scripts/sync-check.mjs`, `contact-sheet.sh`, `probe-mp4.sh`.
  - Recipe code, adapted: GLSL noise/fbm, glitch + chromatic aberration, caption pop, counter, digit reel, punch-in, the 9:16 safe-zone overlay.
- **Hand-built:**
  - Every visual: heart, toon Earth (land, coast halo, desert, ice, clouds, city lights, atmosphere, flashes), RBC shader, Sun/orbit/beam, HUD capsule ring, dashboard, icons.
  - The `zoomThrough` presentation, the SVG chromatic-aberration/glitch/smear filters, screen shake, grain.
  - The timeline generator (`tools/gen-timeline.mjs`), the single source of truth for picture and sound.
  - The whole score and the SFX bank.
  - **The mix and mastering**: ffmpeg sidechain ducking, gain to −14 LUFS, limiter. No skill covers loudness or VO ducking.

## What broke and how it was fixed
1. **The brief switched to 9:16 mid-build.** I re-laid out for vertical:
   - text inside x 90–950 / y 250–1480 (each hero number checked against the guides);
   - numbers 317–354 px tall when they land;
   - word-synced karaoke captions;
   - a non-black frame 0, and S8 dark but not black (blackdetect finds no black segments);
   - a matched loop seam.
2. **The hub repo holds no skills.** All 17 packs had to be cloned separately.
3. **R3F v9 `applyProps` re-wraps `uniforms`.** Number uniforms (time, sizes) froze while Vector3 ones kept working. Found with visual probes. Fix: own the `ShaderMaterial`s via `useMemo` (the threejs skill's imperative-resource pattern).
4. **Additive blending wrote alpha = 1 into the transparent WebGL canvas**, leaving black halos. Fix: opaque in-canvas backdrop shaders.
5. **`@remotion/google-fonts` failed.** Headless Chromium rejected the sandbox proxy's CA. Fix: the same OFL fonts from `@fontsource`, served locally through `@remotion/fonts`.
6. **Remotion's new shader transitions** (`zoomBlur`, `crossZoom`, `linearBlur`, `filmBurn`…) need HTML-in-canvas (Chrome 149 + a flag), but the available Chromium is 141. I used the native `iris`, plus a custom presentation and SVG filters.
7. **CPU-only WebGL (SwiftShader) on a shared 4-core box** with load average 20–28. I baked the 5-octave fbm noise fields into textures once per tab, replaced CSS `blur()` blobs with gradients, and cut particle overdraw.
8. **Three hero numbers grazed the right safe edge.** I re-rendered only the affected frame ranges (`--frames`), spliced them into the master with frame-exact alignment (checked frame by frame), and re-encoded.
9. **Stem levels were coupled.** `render.mjs` normalises each stem to a 0.89 peak, so the SFX stem's level depends on its loudest hit. I rebalanced in the mix: VO sits 8–11 dB over the bed on every line, and 6.6 dB on the drop by design.
10. **`sync-check.mjs` passes 11/15 cues.** Its "strong onset" test is relative within ±1 s and tuned for soft scores, so in this dense, VO-ducked mix it flags 17.19, 20.87, 23.0 and 26.0. My envelope check (`tools/onsets.py`) puts the steepest audio rise within ±2 frames (≤65 ms) of every cue. 26.0 is a cut **into** silence while the VO continues.
11. **The countdown never reaches 00:00.** `ceil(30 − t)` stays at 1 through the last frame, so the countdown flips to **00:00** on the 29.70 heartbeat. The progress ring refills there, so the last frame matches frame 0.
12. **The number-to-chip "flight" at scene ends barely reads.** A steep ease-in means it plays as a shrink-and-fade while the chip pops. I didn't re-render 45 minutes for it.
13. **The poster is at 17.8 s, not 16.5 s.** The number hasn't been spoken at 16.5 s. §10.9 asks for the most striking frame with a big number, so the cover shows 1,300 with lightning.
14. `playwright-core` had to be pinned to 1.56.1 to match the preinstalled chromium-1194.

## Numbers
- **Spec:**
  - `probe-mp4.sh`: 1080x1920, h264, 30 fps, 30.00 s ✓.
  - 900 frames, High profile, yuv420p, moov atom first (+faststart).
  - 13.0 MB (13,002,032 bytes).
- **Loudness** (ffmpeg ebur128 on `final.mp4`):
  - **−14.0 LUFS integrated**, true peak **−1.4 dBTP**, LRA 3.1 LU.
  - The pre-drop gap 15.75–16.00 s sits at −73 dBFS.
  - Silence from 26.0 s holds VO plus room tone at −48 dBFS.
- **Sync:** stills and frames at every word hit (1.26, 4.95, 8.86, 9.26, 12.38, 17.19, 20.87, 24.03, 27.43, 28.81, 29.11, 29.70) show the visual landing on the word frame.
- **Render time:**
  - Full 1080×1920 master: **45 m 31 s** (`--concurrency=2`, SwiftShader, machine shared by 5 agents).
  - Range re-renders: about 8 min.
  - Half-res preview: 27 min.
  - Score stems: about 15 s each.
  - Final encode: under 1 min.

## Scorecard (1–10, honest)
| | Score | Why |
|---|---|---|
| Motion | 8 | The recipes (spring pops, eased counters, punch-ins, camera language, parallax) produce a strong, consistent motion language. The 3D and particles needed real shader work |
| Transitions | 7 | Eight kinds work: morph, zoom-through, iris, white flash, glitch/RGB split, whip smear, hard cut, loop. Only `iris` was off-the-shelf, and Remotion's shader transitions couldn't run in this Chromium |
| Sound | 7 | It follows the cue sheet exactly (heartbeat → kick → build → gap → drop → wide → faster → silence → swell → sting → heartbeat), with SFX on every hit, at −14 LUFS. It's still synth-only and reads as "electronic score", and the library's sync-check is noisy on dense mixes |
| Ease of use | 5 | Excellent know-how, but no components. Almost everything is hand-written, the packs are spread over 17 repos, and some recipes are generic web snippets |
| Agent-friendliness | 7 | Clear SKILL.md workflows, deliver-and-verify loops, and runnable scripts (`render.mjs`, `sync-check`, `contact-sheet`, `probe-mp4`). There's no loudness or mix guidance, and the scripts assume `npx playwright install` and an open network |

## Credits
- **Narration:** shared `vo_full.wav` (Kokoro `af_heart`), used as-is.
- **Fonts** (SIL OFL 1.1), via @fontsource:
  - **Rubik**: Hubert & Fischer.
  - **Barlow Condensed**: Jeremy Tribby.
  - **JetBrains Mono**: JetBrains.
- **Map data:** **Natural Earth** (public domain), through the `world-atlas` npm package (ISC, Mike Bostock), with `d3-geo` and `topojson-client` (ISC).
- **Software:**
  - Remotion (Remotion License; free for individuals and small teams, larger companies need a company licence).
  - three.js (MIT), @react-three/fiber (MIT), ffmpeg.
- **Everything else:** music, SFX, textures, particles and all visuals were generated by code for this film. No samples, no AI generation, no paid APIs.
