# Speech visualization — writing the music of speech

**Status:** idea, logged 2026-08-30. Researched, not built. Prior art: [research.md](research.md).

## The problem

Written English is flat. It keeps the words and throws away the performance: no pitch, no
melody, no rate, no volume, no stress, no pauses. Two people can read the same paragraph
aloud and produce completely different speeches — one electric, one dead — and the page
captures none of the difference. The channel that carries most of the persuasion and music
of speech has no everyday written form.

## The idea

Codify a visual layer on top of plain English that encodes the voice elements directly into
how the text is drawn, so that delivery becomes as readable and copyable as the words:

| Voice element | Visual encoding |
|---|---|
| Pitch / melody | Vertical position — words ride up and down between an upper and a lower wave (the speaker's pitch range), like mountains and waves |
| Volume | Size and weight — text grows to show the body of the voice, shrinks as it trails off |
| Rate of speech | Horizontal density — tight = fast; s p r e a d o u t = slow, deliberate |
| Stress | Stretch — letters spread to show stress on a word; weight or a color pop on the stressed syllable |
| Pauses / breath | Real gaps in the line |
| Tone / color of voice | Hue or ink treatment |

The point of *codifying* it (rather than just animating text prettily) is reproducibility:
**anybody could take the same words, including the voice elements, and talk the same way** —
re-creating a world-class speech, a song's phrasing, a comedian's timing — the way any
pianist can play a score.

## Why it matters

1. **Performance becomes copyable.** Great delivery today dies with the recording. A
   notation makes it teachable and re-performable, the way music became shareable when
   notation was invented.
2. **A training substrate for voice AI.** A codified text↔prosody mapping is exactly the
   kind of paired data a model can train on: TTS that reads a *score* instead of guessing a
   delivery, and speech-to-score transcription in the other direction.
3. **Readable interfaces.** Captions, transcripts, chat, and e-readers could show *how*
   something was said, not just what — including for Deaf and hard-of-hearing readers
   (which is where current academic research on this is most active).

## One format, two renderers — why the visual layer at all

AI voices can already produce expressive delivery, follow coarse inline directions like
`[whispers]`, or clone a delivery from reference audio — so the *machine* does not strictly
need a visual notation. What settles the question is who each half serves:

- **The core artifact is one codified prosody layer attached to text** — measurable values
  for pitch, loudness, timing, and stress, word by word.
- **Renderer 1 — visual, for humans:** the score. People can't read a model's internal
  representation; the visual layer is what makes delivery learnable, copyable, checkable,
  and showable (teaching, captions, transcripts).
- **Renderer 2 — compiled, for machines:** the same layer compiles to SSML / audio tags /
  model conditioning, so any TTS voice can play it back.

The visual half is also the missing **control surface** for AI voices. Today, directing a
voice is vibes: type "more excited", listen, re-roll. A score lets you see the delivery the
model intends and edit it precisely — the difference between telling a photo app "warmer"
and opening the curves editor.

Framed historically: the AI half is the playback engine Steele (1775) and Walker (1787)
fatally lacked; the visual half is the interface today's voice AI lacks. Notation never
made instruments sound better either — it made music copyable between people.

## A sketch

The same sentence, flat and scored:

> it's not what you say, it's how you say it

> it's not **WHAT** you say… <sub>it's</sub> *how* you s&nbsp;a&nbsp;y <sub>it.</sub>

(Crude in markdown — the real thing wants continuous vertical placement, waves, and smooth
size changes — but even the crude version already reads differently, which is the point.)

## Where it came from

Sparked by the early chapters of **Stage Academy by Vinh Giang** — the Vocal
Foundations / Vocal Mastery modules, which treat the voice as an instrument and teach the
ways of speech: rate, volume, pitch, melody, projection. The observation underneath: we
each learned these skills somehow, but there has never been a common way to *write them
down*.

## What the research says (short version)

The idea is old, good, and still unclaimed. People have tried to write the melody of speech
since at least 1775 (Joshua Steele's *Prosodia Rationalis*); Hebrew cantillation has done a
constrained version for over a millennium; linguists have precise expert notations (ToBI,
interlinear "tadpole" transcription); and 2020s HCI research has prototyped almost exactly
this visual mapping (loudness→font weight, pitch→baseline shift, duration→letter-spacing).
**But no unified, layperson-readable, standardized system exists that works in running text
and round-trips with audio.** Every prior attempt stopped at one of: expert-only,
research-prototype, non-visual markup, or informal folk convention. Full findings with
sources: [research.md](research.md).

## What would make this version new

- A **standard, not a demo**: a small, learnable visual vocabulary with a defined mapping to
  measurable acoustics (F0, energy, duration).
- **Round-trip**: audio → score automatically (pitch/energy extraction + forced alignment);
  score → audio via TTS (compile the notation to SSML or inline audio tags). Neither
  direction requires an expert.
- **Runs in plain running text**, degrading gracefully to ordinary prose when the layer is
  stripped.

## Extension: the prosody engine — expressive reading (added 2026-08-30)

A second observation, from how reading aloud works today. Legacy read-aloud (screen
readers, browser "read this page") speaks word by word, neutrally — no tone at all. Newer
AI readers do interpret, but end-to-end and opaquely: the model guesses a delivery in one
shot and you can't see or steer the guess.

Humans don't work that way. A speaker thinks the sentence first, *then* plans the
delivery: which words to stress, where to slow down and speed up, where to drop or raise
the volume, where the melody moves — several channels varied **in parallel**, word by
word. That parallel layering is what creates emotion in the voice, and the emotion is what
creates impact. The difference between an average speaker and Tony Robbins is exactly this
planning — knowing which notes to hit. Stage Academy shows the planning reduces to a
handful of teachable principles, which means it is **codifiable**.

The pipeline this implies:

```
text → prosody planner (the principles as code / an LLM "director")
     → score (the notation — explicit, visible, editable)
     → compile to TTS conditioning → any trained, licensed voice
```

Applications: a real-time expressive reader for any website or PDF (replacing flat
read-aloud), and on-demand audiobooks — license and train an author's voice once, and any
text they wrote plays back with delivery, not just words. The explicit score in the middle
is the difference from today's end-to-end guessing: editable, consistent (same score =
same delivery in any voice), teachable, and inspectable.

Caveats logged alongside, honestly: (1) modern AI readers are no longer flat — the
"neutral reader" premise fully holds only for legacy screen readers; the real gap is
control and consistency, not raw expressiveness. (2) End-to-end models keep improving at
inferring delivery, so for passive listening they may become "good enough" without an
explicit layer — the durable wins are control, re-performability, teaching, and
accessibility. (3) A real person's voice and delivery style require consent and licensing
(ElevenLabs and Speechify already run licensed celebrity-voice programs).

## Open questions

- Granularity: per-word or per-syllable? (Syllable is truer to speech; word is far more
  readable.)
- Static page vs. kinetic (animated) rendering — probably one source format, two renderers.
- How much precision before it stops being readable? Comics prove a handful of crude levels
  are instantly decodable by anyone; ToBI proves full precision is unreadable to almost
  everyone.
- Timbre and register (whisper, vocal fry, breathiness) — the hard residue that pitch,
  volume, and rate miss.
- Ethics of "performance cloning" of real speakers.

## Log

- **2026-08-30** — Idea captured from a voice note. Prior-art research done and written up
  in [research.md](research.md). Logged here and in the personal vault.
- **2026-08-30** — Origin corrected: the course is Stage Academy by Vinh Giang.
- **2026-08-30** — Positioning added (one format, two renderers: visual for humans,
  compiled for machines). Prosody-engine / expressive-reading extension logged, with a
  landscape addendum in [research.md](research.md) (section 10).
