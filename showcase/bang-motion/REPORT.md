# The Next 30 Seconds · bang-motion

Library: bangtutorial/bang-motion v1.19.0 (agent skill: SKILL.md + references/ + assets/ + scripts/), used as if installed.

Output: final.mp4
- Video: 1080×1920, 30 fps, 900 frames, 30.000 s, H.264 High, yuv420p, faststart, 13.2 MB.
- Audio: AAC 192k, 48 kHz stereo, −14.0 LUFS integrated, −1.5 dBTP, LRA 2.9.

Source was in `/home/user/work/bang-motion/project/index.html` (container-local), served by the library's `scripts/serve.py` on :3104. Use `?debug=1` for the scrub panel and `?safe=1` for the safe-zone overlay.

## Choices
- Style direction: **Grainy gradient** (glowing gradient circles, live grain, guiding orb), blended with Sinematik-gelap WebGL bloom for the Earth.
- Opener: **#8 Angka hidup** ("living number"): the countdown is the living number. Candidates were #8, #18 and #2. Opener menu: Suara dulu + Titik cahaya di gelap. Closer menu: Loop mulus + Callback.
- Explainer: **#5 Aksi kontinu** ("continuous action"): one hero circle, and one instrument per fact: ECG → cell tunnel → birth globe → orbit map → light ring.
- Render families: glass orb + neon line, with one deliberate switch "flat dot → 3D Earth" at 12.0 s.
- Fingerprint: `angka hidup · 8 babak · countdown ring / beating rings+ECG / red-disc tunnel / gold dot→globe / storm globe / sun+orbit trail / light ring / tally dashboard→ring · bright 00:30 in crimson pulse ring · loop mulus`.
- Transitions (9 kinds):
  - match cut on the circle (4.0);
  - zoom-through into the heart (8.0);
  - morph cell → gold sphere (12.0);
  - pull-back reveals (12.0, 20.0);
  - white flash + RGB glitch + shake (16.0 / 17.19 / 18.4 / 19.2);
  - whip smear (22.8–23.3);
  - hard cut to dark + silence (26.0);
  - iris through the ring (27.0);
  - ring collapse into the final 0 (29.2–29.7).

## Library features used
- **SKILL.md:** style brief (written into the page header), three candidates, fingerprint, the 8 anti-PPT checks, determinism (everything is a function of `tl.time()`).
- **anti-ppt.md:** ≤2 text levels, motivated camera, never reveal the world's edge (auto zoom compensation cosθ+(H/W)sinθ).
- **opener-konsep.md:** concept #8, opener/closer menus, carried-transition menu.
- **explainer.md:** aksi-kontinu rules, counters/odometer, 9:16 notes, VO-sync procedure.
- **architecture.md:** absolute timeline, CSS initial states, state-driven WebGL, `window.OPENER`, `?debug` / `?clean`.
- **assets/starter-opener.html:** stage + fit, `#world` rig (CAM{s,fx,fy} from techniques §3b), makeBlur/blurTween verbatim, door functions, light leak, vignette, UnrealBloomPass with high threshold, autoplay/loop, seek.
- **techniques.md:**
  - §1 `color` emphasis used as the karaoke highlight; §3 push-through; §3b punch-ins; §4b breathing camera.
  - §4c: #1, #6, #9.
  - §7 dust → 1,400 embers; §7b palette behind cuts; §7c #6/#7/#4.
  - §7d grainy gradient: the library's exact grain shader line, plus 12-jumps/s DOM grain.
  - §9 counters; §10 pitfalls.
- **scripts/serve.py:** dev server on :3104.
- **scripts/vo-pauses.html:** run headless on vo_full.wav. SEG = [0.81, 4.26, 8.21, 12.21, 16.36, 20.16] matches vo_timeline line starts within ≤10 ms; ffmpeg silencedetect agrees.
- **scripts/snap.mjs → tools/snap.mjs:** about 150 stills inspected.
- **scripts/export-frames.mjs → tools/render.mjs:** frame-exact export.

## Native vs hand-built
**Native** (restyled):
- stage/rig/timeline, doors, motion blur, leak, bloom, grain;
- push-through, whip, breathing camera;
- debug/clean/seek;
- server, snap/export, VO pause detection.

**Hand-built:**
- All audio:
  - `audio/score.py` synthesizes heartbeat, kick-as-heartbeat, hats, bass, supersaw pads, 124 pentatonic plinks, riser, snare roll, thunder + sub drop, 67 zaps, doppler, whip, lap zaps, reverse cymbal, bell sting, room tone.
  - `audio/master.py`: VO-keyed ducking (music −7 dB / SFX −5.5 dB; VO sits 9.6 dB over the bed), 28 Hz HPF, −14 LUFS, 4× oversampled TP limiter.
- Three.js content:
  - Natural Earth land mask into a custom globe shader (graticule, storms, lightning light, city lights, rim);
  - 1,600 biconcave cells;
  - hero-cell sphere morph;
  - 125 population-weighted birth dots + ripples;
  - lightning sprites + projected 2D bolts;
  - Sun / orbit / trail;
  - 10 light-lap ring shaders.
- Platform layer:
  - karaoke captions (the library defaults to none);
  - countdown HUD;
  - tally rail + rolling dashboard;
  - odometer columns;
  - RGB-split filter, DOM shake, ECG;
  - 2D FX layer;
  - safe-zone layout.

## Problems and fixes
1. **The starter renders every rAF while paused,** which made each capture take ~15 s in SwiftShader. Fix: render only while playing. Now ≈5 s/frame at load average 18–28.
2. **Stale frames.** The `seek → rAF → seek → screenshot` pattern sometimes captured the previous frame. Fix: seek → 2×rAF → screenshot, plus a 1-px getImageData to commit the 2D canvas.
3. **No vertical rules.** The library's `.safe(.78)` leaves about 230 px at the bottom, versus 440 px covered by app UI. All text is hand-placed in x 90–950 / y 250–1480, and numbers are centred on x = 520.
4. **Numbers ≥300 px inside 860 px.** Solved with Big Shoulders Display sized from measured metrics ("1,300" at 370 px = 855 × 301).
5. **The 9:16 FOV cropped the globe.** I reframed from geometry and tilted the tropics toward the camera; S6 pose solved for Sun at y≈330 and Earth at y≈1080.
6. **Roll and shake exposed the world's edges.** Fixed with auto zoom compensation.
7. **The HUD disc dimmed the big numbers.** It now fades with the digits.
8. **Two overlaps in the full render** (2.3–2.6 s and 27.0 s). I re-rendered only frames 66–80 and 796–818 and spliced them frame-exactly.
9. **AAC overshoot.** −1.2 dBTP became −0.5 after AAC; I re-mastered at −2.3, giving −1.5.
10. **Grain vs the 14 MB cap.** The library says grain needs CRF 10–12. At 3.3 Mbps the grain softens (SSIM-Y 0.55 vs HQ), with no banding.
11. **Tooling friction:**
    - the scripts need full puppeteer, 60 fps PNG folders and a server; I patched them to use puppeteer-core, 30 fps and streaming to ffmpeg;
    - docs are Indonesian only;
    - the file:// promise breaks with vendored ES modules;
    - vo-pauses merges lines with gaps under 0.45 s, so word hits came from vo_timeline.json.

## Render time
- Capture: 2 workers × 450 frames in 2,532 s and 2,428 s, in parallel (≈42 min wall, ≈5.5 s/frame on a shared box).
- Patches: 121 s. 2-pass encode: ~7 min. Audio: ~22 s.
- **Total export ≈52 min.** Build and iteration took about 2 h more.

## QA
- **ffprobe:** 1080×1920, 30/1, 900 frames, 30.000 s, H.264 High, yuv420p, AAC LC 48 kHz stereo, faststart.
- **ebur128:** I −14.0 LUFS, TP −1.5 dBFS.
- **blackdetect:** none; S8 is dark crimson with the ring and captions visible.
- **Sync:** the first frame at or after each word (30 1.26, 35 4.95, 70 8.86, million 9.26, 125 12.38, 1,300 17.19, 900 20.87, 224 24.03, this 27.43, 30 28.81, count 29.11, lub 29.70) shows the final value or the slam starting (≤1 frame). SFX use the same exported event times.
- **Loop:** last frame 00:00 + ring + pulse matches frame 0 (00:30). The hook text is readable by 0.36 s.
- **Poster:** frame 522 (17.4 s), 0.1 s past the default window, because 16.5 is mid-roll and 17.2–17.3 is flash-washed.

## Scorecard
| | Score | Why |
|---|---|---|
| Motion | 8 | The rig, blur and doors make it move like video, but all the 3D and particles are hand-built. |
| Transitions | 7 | Great menus; push-through and whip worked as written. Iris, morph, glitch and collapse were hand-built. |
| Sound | 2 | The library has no audio; everything is hand-built. |
| Ease of use | 5 | ~5.9k lines in Indonesian, 16:9-only starters, scripts need patching. |
| Agent-friendliness | 7 | Mechanical checks and OPENER.seek, but the paused render loop and stale capture cost hours. |

## Credits
- Fonts (OFL 1.1, via Fontsource): Big Shoulders Display (Patric King / XYZ Type), Bricolage Grotesque (Mathieu Triay), JetBrains Mono (JetBrains).
- Land: Natural Earth 1:50m (public domain), via world-atlas (ISC) + topojson-client (ISC).
- Libraries: GSAP 3.12.5 (no-charge licence), Three.js r161 (MIT), bang-motion (MIT, © Bang Tutorial).
- VO: vo_full.wav (Kokoro af_heart), used as-is.
- All music and SFX were synthesized from scratch. No AI services or paid APIs were used.
