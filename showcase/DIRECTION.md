# THE NEXT 30 SECONDS — Creative Direction

One script, one timeline, one narration, made five times with five motion libraries.
Every video runs exactly 30 seconds, so the comparison is fair: same story, same beats, same
voice, with each library's own look, recipes and sound.

---

## 1. Logline

> *"In the next thirty seconds…"* The video counts down the real time you spend watching it, and
> shows what happens in your body, to humanity, to the planet and across the cosmos in that
> time. Then it turns back to you: *"All of that… while you watched this. Make the next thirty count."*

## 2. Why it holds attention start to finish

| Device | How it works here |
|---|---|
| **Open loop in frame 1** | A live countdown `00:30` starts at frame 0 and reaches `00:00` on the last frame. Viewers stay to find out what happens at zero. |
| **Second person** | "Your heart… your body…" The viewer is the subject before the video zooms out. |
| **Escalating scale** | Body → humanity → planet → solar system → speed of light → back to *you*. Every scene is bigger than the one before. |
| **A number every 4 seconds** | Each scene pays off one surprising number that lands exactly on the spoken word. That's a steady stream of small rewards. |
| **The drop at 16.0s** | Music builds from heartbeat-only to a full drop on the lightning scene, mid-video, where retention usually sags. |
| **Silence before the payoff** | At 26.0s everything cuts to silence. A sudden absence of sound pulls attention back. |
| **Seamless loop** | The video ends on the same single heartbeat it opens with, so autoplay loops feel continuous and the replay rate goes up. |

## 3. The visual through-line: **one circle**

Every scene is built around a circle, and every transition is a **match cut on that circle**:

`pulse ring (heart)` → `red blood cell` → `a single glowing dot that multiplies into newborn dots on a globe`
→ `lightning-lit Earth` → `Earth on its orbit around the Sun` → `a ring of light around the planet`
→ `the "0" in 00:00` → `the heart pulse again (loop)`

Libraries can interpret the circle in their own style (painted, printed, neon, data-viz, 3D),
but the circle must carry the eye across every cut.

## 4. Persistent HUD

- **Countdown:** `00:30` → `00:00` in real time (`ceil(30 − t)`), small, monospaced, top-right
  (or the library's equivalent). Visible the whole video. Ticks on whole seconds.
- **Progress:** a thin ring or bar that drains with the countdown.
- **Tally rail (optional, encouraged):** each scene's number stays as a small running counter
  that keeps ticking after its scene ends. At 27.0s the payoff shows all of them at their
  final values in one dashboard.

## 5. Timeline: 120 BPM · 1 beat = 0.5s · 1 bar = 2.0s · 30fps (frame = t × 30)

The narration is **already recorded** (`_shared/vo/vo_full.wav`, Kokoro `af_heart`), and its word
times are in `_shared/vo/vo_timeline.json`. Visual hits must land on those word times (±2 frames).

| Scene | Time | VO line (start → end) | Key word hits | Visual | Palette | Sound |
|---|---|---|---|---|---|---|
| **S1 Hook** | 0.0–4.0 | "In the next thirty seconds…" (0.80→2.18) | "30" @1.26 | Black. One heartbeat pulse ring at 0.0. Words build up one at a time. **30** slams in on the word, huge. The countdown snaps into the HUD at ~2.5s and the ring tightens. | Black, white, one crimson pulse | 0.00 sub "lub", 0.30 "dub". Low drone. **Impact** at 1.26. Riser 2.5→4.0. |
| **S2 Heart** | 4.0–8.0 | "Your heart will beat thirty-five times." (4.25→6.20) | "35" @4.95 | The pulse ring becomes a beating heart (or an abstract pulse). Counter 0→35 lands on 4.95 and keeps ticking at ~70 bpm. | Crimson / ember | **Kick enters at 4.0** and doubles as the heartbeat. |
| **S3 Blood** | 8.0–12.0 | "Your body will make seventy million new red blood cells." (8.20→10.88) | "70" @8.86, "million" @9.26 | Push in on the heart, through it, into a stream of thousands of red discs (particles, ≥1,000). Counter rolls to **70,000,000**. | Deep red, plasma pink | Hats + bass pulse. Soft "bubble" ticks on cell bursts. |
| **S4 Babies** | 12.0–16.0 | "About a hundred and twenty-five babies will be born." (12.20→14.78) | "125" @12.38 | One cell becomes a single warm dot. Dots pop up across a globe or map, about 125 in total. | Warm gold, soft pink, cream | Warm pad and chords. A pentatonic **plink per dot**. **Riser + snare roll 14.0→16.0**, with a ⅛-beat silence gap at 15.75. |
| **S5 Lightning** | 16.0–20.0 | "Lightning will flash thirteen hundred times." (16.35→18.42) | "1,300" @17.19 | **THE DROP.** White flash frame at 16.0. Storm-lit Earth with strike flashes all over it. Glitch/RGB split, camera shake. Counter rolls to **1,300**. | Electric white, violet, ultramarine | **Drop at 16.0**: thunder crack, sub drop, full beat. Zaps on flashes. |
| **S6 Orbit** | 20.0–23.0 | "Earth will fly nine hundred kilometers around the Sun." (20.15→22.81) | "900" @20.87 | Big **pull-back**: Earth shrinks onto its orbit line around the Sun, with a motion trail. Counter **900 km**. | Deep blue, teal, solar orange | Wide pad. Doppler whoosh on the pull-back. |
| **S7 Light** | 23.0–26.0 | "Light will circle the planet two hundred and twenty-four times." (22.95→26.01) | "224" @24.03 | Fastest scene: a beam of light wraps the planet again and again and becomes a blinding ring. Counter **224×**. Speed lines, motion blur. | Cyan, white-hot | 1/16 hats, zaps. **Reverse cymbal into 26.0.** |
| **S8 Payoff** | 26.0–30.0 | "All of that… while you watched this." (26.25→27.93) · "Make the next thirty count." (28.25→29.64) | "this" @27.43, "30" @28.81, "count" @29.11 | **Hard cut to black and silence at 26.0.** At 27.0 the tally dashboard shows all five numbers. At 28.25 the final line in big type. The light ring collapses into the **0 of 00:00**. Single heartbeat pulse at 29.7, which loops back into frame 0. | Black, white, one crimson pulse | **Silence at 26.0** (VO plus faint room tone only). Soft chord swell from 28.0. Sting on "count" at 29.11. **Heartbeat lub-dub at 29.70**. |

## 6. What each video must show off (the capability test)

Use **as much of your library's native vocabulary as possible**. This is a breadth test.

- **Motion:** kinetic type synced to the words · rolling number counters · a particle system
  (≥1,000 elements) · a camera move in every scene (push, pull, orbit, whip) · ≥3-layer parallax ·
  at least one 3D or 2.5D element (the Earth) · varied easing (spring, expo, overshoot) ·
  motion blur or smear frames.
- **Transitions (use ≥6 different kinds):** match cut on the circle · zoom-through · whip pan or
  smear · white flash · glitch or RGB split · iris or circle wipe · morph · hard cut to black.
- **Post / FX:** glow or bloom · film grain or noise · vignette · chromatic aberration on the drop ·
  screen shake on the drop.
- **Sound:** an original score that follows the cue sheet above (heartbeat intro → kick at 4.0 →
  build → **drop at 16.0** → wide → faster → **silence at 26.0** → swell → heartbeat) · SFX on
  every transition and number hit · VO ducked under music by sidechain or volume automation.

## 7. Facts (keep the numbers honest)

| Claim | Basis | 30-second value |
|---|---|---|
| Heart beats ~35 times | Resting adult ≈ 70 bpm | 35 |
| ~70 million new red blood cells | Body makes ≈ 2–3 million RBC per second (commonly cited ≈ 2.4 M/s) | ≈ 72 M → "70 million" |
| ~125 babies born | ≈ 132 M births/yr (UN WPP) ≈ 4.2 per second | ≈ 126 |
| Lightning flashes ~1,300 times | NASA LIS/OTD global rate ≈ 44 flashes/s | ≈ 1,320 |
| Earth travels ~900 km around the Sun | Orbital speed ≈ 29.8 km/s | ≈ 894 km |
| Light circles Earth 224 times | 299,792 km/s × 30 s ÷ 40,075 km | ≈ 224.4 |

## 8. Technical spec (all five videos)

- **1920×1080, 30 fps, duration exactly 30.00s** (900 frames, never longer).
- H.264 High, yuv420p, `-movflags +faststart`, aim for ≤ 14 MB (CRF ~20, or cap the bitrate).
- AAC 192 kbps, 48 kHz stereo. **−14 LUFS integrated, true peak ≤ −1 dBTP.** VO about 8–10 dB above the music bed.
- Narration: use `_shared/vo/vo_full.wav` as-is (already placed on the timeline), or the per-line
  WAVs in `_shared/vo/lines/` at the start times in `vo_timeline.json`. Don't re-voice it.
  The same narrator across all five keeps the comparison fair.
- Every font, sample and asset must be CC0 / CC-BY / OFL or self-generated. Credit them in the REPORT.

## 9. Deliverables per library: `showcase/<slug>/`

- `final.mp4`: the 30-second film
- `poster.jpg`: frame at 16.5s (the drop)
- `contact.jpg`: contact sheet with one frame per scene (8 tiles)
- `REPORT.md`: which recipes/components/skills from the library were used (with paths), what was
  native vs hand-built, what broke and how it was fixed, render time, and an honest 1–10
  scorecard (motion · transitions · sound · ease of use · agent-friendliness)

| Slug | Library | Suggested look |
|---|---|---|
| `hyperframes` | heygen-com/hyperframes (+ registry) | Clean kinetic editorial with shader transitions, GSAP and a Three.js Earth |
| `iart-motion-skills` | iart-ai/motion-skills | Kurzgesagt-like explainer pulling from several packs (kinetic type, data-viz, 3D) |
| `lemo-opuscar` | lemomo-ai/lemo-opuscar | One of its 43 film styles, scored with its real-instrument sampler |
| `bang-motion` | bangtutorial/bang-motion | One of its 10 style directions plus an opener concept for the hook |
| `farhan-motion-video` | farhan-syah/motion-video-skill | Data-rich motion graphics with its icon kit and Natural Earth maps, plus motion-synthesized SFX |
