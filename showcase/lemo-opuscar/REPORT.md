# THE NEXT 30 SECONDS · lemo-opuscar

**Style: Sci-fi Hologram HUD** (`styles/hologram-hud/`, one of the library's 43). The film is vertical 1080×1920 at 30 fps, exactly 30.000 s (900 frames), built for Shorts, Reels and TikTok.

| Deliverable | Measured |
|---|---|
| `final.mp4` | 1080×1920 · 30 fps · 900 frames · 30.000 s · H.264 **High**, yuv420p, BT.709 · moov before mdat (+faststart) · AAC-LC 48 kHz stereo ~196 kbps · **13.84 MB** |
| Loudness | **−14.2 LUFS integrated**, LRA 2.4 LU, true peak **−1.4 dBTP** (ffmpeg `ebur128=peak=true`) |
| `poster.jpg` | frame at **17.5 s** (see §5.9) |
| `contact.jpg` | 8 vertical tiles, one per scene (1.4 / 5.3 / 10.0 / 13.6 / 17.5 / 21.6 / 25.2 / 27.8 s) |

Project source was in `/home/user/work/lemo-opuscar/next30/` (container-local): one-command `build.sh`, `TREATMENT.md`, `CREDITS` and `next30.srt`.

## 1. Why this style

The film is a journey through scale (body → planet → cosmos → you) with a live countdown. I picked Hologram HUD because most of what the brief asks for is already part of its grammar:

- **Countdown HUD.** A live status readout is standard furniture in this style, so the 00:30 → 00:00 dial belongs in the frame instead of being pasted on top.
- **Numbers.** The style's signature move is rolling digits: values scramble, lock right to left, and turn into the accent colour on the lock frame. Every scene in this film pays off one number.
- **Tally rail.** The style's chip dock is exactly that; here the chips tick live.
- **The drop.** The style's sound palette already includes "drop = 808 glide + wide saw chord", "one beat of true digital silence" and "glitch of three frames, once, on the biggest change". Those map straight onto the cue sheet's 15.75 gap, the 16.0 drop and the 26.0 silence.
- **The circle through-line.** The projector pad (concentric rings) is a constant of the style. The chain of match cuts is: pulse ring → pad → aorta rings → vessel tunnel → loupe iris → birth ping rings → orbit dial → light rings → ghost ring → the 0 of 00:00.
- **On a phone** it is striking: a near-black stage, additive glowing wireframes and one warm accent. It also looks nothing like the other four looks in the brief.

**Colour.**
- One cold hue, ice cyan. It drifts within cold hues by mode: violet for the storm, teal for the orbit, white-cyan for the light.
- The accent is amber and is used for locked values only.
- The style's single-colour exception ("keep") is crimson for "you": the pulse ring, the heart and the blood.

That is how I adapted the brief's per-scene palette without breaking the style.

## 2. Workflow (the library's director method, end to end)

I followed `AGENTS.md` step by step:

1. **Brief.** All up-front answers came from DIRECTION.md. The voice was supplied, and there was no storyboard stop.
2. **TREATMENT.md, before opening the demo.** It has three candidate structures, a benchmark (*Powers of Ten* plus the vertical counter-shorts genre), a shot list, a beat sheet against word frames, a cue map (120 BPM, D minor) and a sound-design table.
3. **Look.** Review stills came from the real drawing code (`core/render/still.mjs` and `sheet.py`) and were inspected visually. There were four review passes over all scenes, plus 100 % crops.
4. **Produce.** Events → score → mix → render → master → final encode.
5. **Self-check (DIRECTOR §11, TECHNIQUE §8).** Contact sheets, frames at every word hit, asr_check, loudness, blackdetect and freezedetect, readcheck, the "not the demo again" comparison and the sign-off grep.

**Scene → native technique**

| Scene | Driven by |
|---|---|
| S1 Hook | Pad in plan view as a dial (`drawPad`); the crimson pulse ring is a 3D ring on the pad; `rollText` resolves "IN THE NEXT / 30 SECONDS" by 0.2 s; the 30 slams with a spring overshoot; the dial whip-docks to the HUD; a crane from plan to 3/4; scan-plane growth builds the heart. |
| S2 Heart | `Holo.draw` on an in-memory heart with real CAD topology (tubes for aorta, pulmonary trunk, vena cava); target lock with tag and 3-frame flash; leader; local explode (shells slide along z, internal hot valves glow); the heart pulses on the lub-dub kick. |
| S3 Blood | Zoom-through: push into the heart, near-plane cull, flash. Inside: a vessel tunnel with 1,400 tumbling biconcave discs plus a burst that grazes the lens. A loupe (frame-in-frame, two scales) on a locked cell, whose iris closes into an amber dot. |
| S4 Births | Globe (lat/long grid plus Natural Earth coastlines), scan-in, turntable spin, 125 amber dots with ping rings, a live "BIRTHS LOGGED" counter. |
| S5 Drop | White frame; the single 3-frame glitch; RGB split decaying over 0.45 s; shake; spring punch-in; shockwave ring; 120 bolts with double flashes; storm bands; a whip-orbit with real 5-sub-frame motion blur. |
| S6 Orbit | Log-zoom pull-back with blur to a plan view; the orbit is drawn as a ticked dial; a glowing motion trail; the Sun drawn by the engine (camera-offset trick); a target box "EARTH · 29.8 KM/S". |
| S7 Light | Whip back in; five inclined beam rings whose speed is integrated from 1 to 7.47 laps/s (224 laps ÷ 30 s); engine glow; speed lines; the solid-hologram Fresnel pass, used once; white-out. |
| S8 Payoff | The style's power-down ending as a hard cut: HUD off, dial and captions stay. A ghost ring collapses into the last 0. The chips become the dashboard. Power returns on the heartbeat, and the last frame matches frame 0. |

**Transitions (10 kinds):** match cut on the circle, scan wipe, zoom-through, morph (cell → dot), iris, white flash, glitch/RGB split, whip with motion blur, log-zoom pull-back, hard cut to dark.

**Post / FX:** engine bloom (two glow levels), vignette, chromatic aberration and shake on the drop, film grain (ffmpeg `noise`, the library's mux grain), and three-layer parallax (dot grid, subject, HUD rulers).

**Brief checklist:**
- Kinetic type synced to words: yes.
- Rolling counters: yes.
- Particles: 1,400 cells (≥ 1,000).
- A camera move in every scene: yes.
- 3D element: the 2.5D wireframe Earth.
- Easing: spring, expo and overshoot.
- Motion blur: sub-frame accumulation.

## 3. Library features used (paths in lemomo-ai/lemo-opuscar)

| Feature | Path | How it was used |
|---|---|---|
| Method | `DIRECTOR.md`, `TECHNIQUE.md`, `AGENTS.md`, `plugin/skills/lemo-opuscar/SKILL.md` | Followed in skill mode; the project lives outside the repo and is served at `/@film/`. |
| Style | `styles/hologram-hud/STYLE.md`, `DEMO.md` | Read in full. The demo was opened only after the treatment existed. |
| Setup | `plugin/skills/lemo-opuscar/scripts/setup.sh deps music` | npm, `.venv` and numba. |
| Samples | `tools/fetch.sh instruments vcsl` (271 MB) | The smallest pack covering drums, cymbals, mallets, harp and bowed vibes. |
| Render pipeline | `core/render/still.mjs`, `video.mjs` (`--size 1080x1920 --fps 30 --workers 2`), `events.mjs`, `readcheck.mjs`, `sheet.py`, `srt.py`, `serve.mjs`, `page.mjs` | All rendering went through these. |
| Engine | `styles/hologram-hud/demo/engine/holo.js`, `hud.js` | Copied into the project, as the library requires. One patch: a near-plane cull. |
| Sampler | `core/audio/sampler.py` (`render`, `hit`, `note`, `room`, `credits`, `seed`) | 244 sampled notes from 14 VCSL instruments. |
| Modal synthesis | `core/audio/pluck.py` (`kalimba`, `music_box`) | The births plinks layer and the "count" sting. |
| Foley and mix | `core/audio/sfx.py` (`add`, `compress`, `limit`, filters, `noise`, `brown`) | All foley is procedural, driven by `window.EV` → `events.json`. |
| Voice check | `core/tts/asr_check.py` (faster-whisper base.en) | 9/9 lines pass, with `asr` overrides for "125", "1,300" and "watch". |
| Master | `core/render/mux.sh` | Failed on this machine (§5.3). `final.sh` reproduces its chain. |

**Native vs hand-built**

- **Native:** engine projection and rendering, glow, pad, scan plane, target box, leader, rolling text, plates and glitch; the render pipeline; event export; sampler, pluck and sfx; asr_check; sheet and srt.
- **Adapted in style:**
  - The countdown dial (the style's status readout, made into a hero element that docks).
  - Karaoke captions: the style's subtitle plate with voiceprint bars, with the active word in inverse video (the HUD tag look).
  - The dashboard (the chip dock grown into rows).
  - The vertical layout: cards on the bottom band, chips on the top band, everything inside the safe zone.
- **Hand-built:** the heart, globe and sphere models (`models.js`), the vessel and cell renderer, lightning, beam rings, the RGB split, the portrait vignette, `score.py`, `mix.py` (modelled on the demo's mixer) and `final.sh`.

## 4. Sound

**Cue sheet, followed exactly**
- **0.00 / 0.30:** sub-heartbeat lub-dub, then a drone (detuned saws plus bowed vibraphone).
- **1.26, the "30" impact:** gran cassa, clash, 808 sub and reverse air.
- **2.5 → 4.0, riser:** a sus-cymbal crescendo cut so its peak lands on 4.0, plus a noise sweep and a saw glide.
- **4.0:** the kick enters as a lub-dub heartbeat, with an 8th-note saw bass.
- **S3:** hats go from 8ths to 16ths.
- **S4:** warm Fmaj9 / Gm7 chords with harp, and a pentatonic plink per newborn-dot cluster (glockenspiel, hand chimes, pluck kalimba).
- **14.0 → 15.75:** an accelerating snare roll with cymbal swell and riser, then true digital zero from 15.75 to 16.0.
- **16.0, the drop:** thunder crack, 808 glide D2 → D1, four-on-the-floor, claps on 2 and 4, 16th hats, wide saw stabs and a zap per strike.
- **S6:** half-time, wide pad, harp sweep, a tubular bell on "900", a Doppler whoosh.
- **S7:** 16th hats, a ping-pong saw arp (1–4 kHz scooped out for the voice), toms, and a reverse cymbal into 26.0.
- **26.0:** hard silence, with only the voice and projector-hum room tone.
- **28.0:** the swell starts.
- **29.11, "count":** the sting (hand chimes, glockenspiel, music box).
- **29.70 / 29.88:** the heartbeat.

All musical onsets sit on the 1/16 grid (asserted in `score.py`), except the word-locked hits.

**Foley on every transition and number hit:** frame-rate roll ticks, the lock sound (thump, clack and a two-tone beep in key), an amber confirm chime, whooshes, scans, a servo, cell bubbles, zaps, a glitch burst, the iris, ignition and a power-down click.

**Mix**
- The voice is used as supplied and compressed.
- Music and foley duck under it with a held envelope; lock transients escape the duck.
- A per-line balance keeps the voice 8.1–9.7 dB above the music in every line (10.3 dB overall in voiced regions).
- The music's 20–120 Hz band sits about 2 dB under the mids.

**Sync (sound onset minus word frame, in frames):**

| Hit | Δ frames |
|---|---|
| 30 | +0.25 |
| 35 | +0.55 |
| 70 | +0.27 |
| million | −0.72 |
| 125 | −0.36 |
| 1 | +0.35 |
| ,300 | +0.57 |
| 900 | −0.04 |
| km | −0.05 |
| 224 | +0.15 |
| count | −0.24 |
| heartbeat | −0.01 |

The A/V offset of the final file against the mix is 0.00 ms. Whisper on the final mix transcribes every line correctly.

**Caveat:** I cannot listen. Every audio judgement here is numeric (RMS, bands, onsets, ASR).

## 5. Problems and workarounds

1. **setup.sh tries to download a browser.** It runs `playwright install chromium-headless-shell` (playwright-core 1.63 wants build 1243; the machine has 1194), which was forbidden here. A node PATH shim skipped only that step, and the renderer used `PLAYWRIGHT_CHROME` pointing at the preinstalled headless shell.
2. **Random server port.** The library's server binds a random port, but only 3103 was allowed. A three-line `node --import` preload maps `listen(0)` to 3103. As a result, only one render tool can run at a time.
3. **mux.sh rejects audio shorter than about 60 s on ffmpeg 6.1.** loudnorm's look-ahead makes the last `out_time` lag about 2.9 s, so it reported "only 27.1 s decoded" for a valid 30 s WAV. `final.sh` repeats its chain (two-pass linear loudnorm, grain) and also meets the spec (AAC 192k, H.264 High, BT.709).
4. **Size.** CRF 21 gave 51 MB. The final is a two-pass encode at 3.43 Mbps with grain at strength 1, coming in at 13.84 MB. Dark gradients are slightly soft at 100 %; the type stays clean.
5. **readcheck fails all caption chunks by design.** It enforces holds of 1.8 s or more; §10 asks for 3–4-word karaoke. One 0.38 s chunk was merged.
6. **Near-plane cull added to the project's engine copy** (marked `[next30]`), so push-throughs don't smear.
7. **Fixed during review:**
   - Frame 0 was too scrambled.
   - Two karaoke words lit up at once.
   - The lightning was invisible.
   - Dashboard rows crossed each other and were still rolling on "this".
   - There was an empty beat at 2.4–3.0 s.
   - The RBC loupe looked flat.
   - The orbit trail was faint.
   - "1,300" crossed the safe edge at x 986 (now x 96–950, even at peak punch).
   - Corner telemetry text sat outside the safe zone; removed.
   - The low end was 7 dB above the mids.
   - The final sting and swell were inaudible (18 dB under the voice).
8. **"watch" vs "watched".** The narration says "watch" (Whisper and the timeline agree); the script says "watched", and the caption uses the script's "WATCHED". Re-voicing wasn't allowed.
9. **Poster at 17.5 s.** At 16.5 s no number is on screen yet. §10 asks for a frame with a big number, and at 17.5 s, 1,300 has just locked in amber.
10. **Black frames.** Only the intended dark cut at 26.00–26.27 s (dial and chips lit). No freezes over 0.5 s; the only silence is 15.75–16.0.
11. **Not a copy of the demo.** The demo is an e-bike spec film. Five of the six comparison points differ: structure, opening, signature shot, camera path and ending. The score shares the style's drop and silence tools. The sign-off grep is clean.

## 6. Render time

- **Stills:** 70–750 ms each.
- **Full render:** 900 frames, Canvas 2D, 2 workers, on a 4-CPU machine shared at load average up to ~25. Each pass took 5 m 26 s to 8 m 40 s; whip frames cost five times as much.
- **Final two-pass encode:** 6.5–10 min.
- **Score and mix:** about 15 s.
- **Totals:** 4 full renders and about 120 review stills.

## 7. Scorecard

| Area | Score | Why |
|---|---|---|
| Motion | 8 | Rich native vocabulary: locks, explode, loupe, scan growth, blurred whips, a 2.5D Earth. There is no shaded 3D (by style). The cells, beams and lightning were hand-built. |
| Transitions | 7 | Ten kinds, and the circle carries every cut. Some are simple, and the zoom-through is busy. |
| Sound | 7 | Real CC0 instruments, cue-accurate, foley on everything, a measured balance, sync within ±1 frame. Unheard: every check was numeric. |
| Ease of use | 6 | Excellent docs and tools. Against that: the browser download, the random port, the mux.sh bug, an engine that lives in `demo/`, docs partly in Chinese, and no partial-range render. |
| Agent-friendliness | 8 | A clear page contract, deterministic tools with exit codes, events.json feeding the mix, asr_check and readcheck. The treatment-first method measurably helped. |

## 8. Credits

- **Engine:** lemo-opuscar `styles/hologram-hud/demo/engine/` (MIT), copied and lightly patched.
- **Fonts (SIL OFL 1.1, self-hosted):** Rajdhani (Indian Type Foundry) and Share Tech Mono (Carrois Apostrophe), from google/fonts.
- **Samples (CC0 1.0):** VCSL, by Versilian Studios / Sam Gossner. Instruments: claps, clash, glockenspiel, gran_cassa, hand_chimes, harp, hihat, shaker, snare2, sus_cymbal, toms, triangle, tubular_bells and vibraphone_bowed. The line from `sampler.credits()` is: "Samples (CC0): Versilian Community Sample Library (Versilian Studios)".
- **Synthesis:** `pluck.py` modal synthesis; all other synthesis and foley are original numpy code.
- **Map:** Natural Earth 1:110m land (public domain).
- **Narration:** the supplied `vo_full.wav` (Kokoro-82M, voice `af_heart`, Apache-2.0), used as-is.
- No paid APIs, no AI generation, no stock footage.
