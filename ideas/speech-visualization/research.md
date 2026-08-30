# Prior-art research: has anyone tried to write the music of speech?

Researched 2026-08-30 (web search). Question: does a system already exist that encodes
pitch, melody, rate, volume, and stress of speech visually into written text — readable by
ordinary people, precise enough to re-perform from, and usable to train voice models?

## Verdict

**The idea is real, old, and repeatedly reinvented — and still unclaimed.** Humans have
been trying to write the melody of speech for at least 1,400 years, and the specific modern
form of this idea (typography modulated by prosody) is an active research area right now.
But every existing attempt stops at one of five walls:

1. **Expert-only** — linguists' notations are precise but unreadable without training (ToBI,
   interlinear transcription).
2. **Lost to history** — the 18th-century elocutionists built exactly this and it faded.
3. **Research prototype** — the modern HCI work (prosodic fonts, speech-modulated captions)
   validates the mapping but never became a standard or product.
4. **Non-visual** — the machine encodings (SSML, audio tags) codify prosody as markup words,
   not visible form.
5. **Informal** — comics and internet typography prove laypeople can read visual prosody,
   but the conventions are folk, coarse, and not tied to measurable acoustics.

No one has shipped the combination: **a unified, layperson-readable, standardized visual
notation for prosody in running text that round-trips with audio (speech → score → speech)
and is used as a human/machine interchange format.** That gap is exactly what this idea
targets.

---

## 1. The ancients got here first (in a constrained form)

The oldest writing systems for "how to say it aloud" are marks over sacred text:

- **Ekphonetic notation** — symbols added to lectionary readings of scripture as memory
  aids for melodic recitation ("quasi-melodic recitation of text"). Introduced into Syriac
  by Joseph Huzaya in the early 6th century; best known from Byzantine chant.
  ([Wikipedia](https://en.wikipedia.org/wiki/Ekphonetic_notation))
- **Hebrew cantillation (ta'amei ha-mikra)** — the Tiberian Masoretes put a mark on *every
  word* of the Hebrew Bible encoding a melodic motive plus phrasing and pauses; the style is
  "closer to heightened speech or declamation than to fixed song."
  ([Wikipedia](https://en.wikipedia.org/wiki/Hebrew_cantillation)) Still read fluently every
  week in synagogues worldwide — the strongest existence proof that **an entire lay
  community can learn to read melody off text**.
- **Neumes → the musical staff** — Western music notation itself evolved from squiggles
  above chanted words into heighted marks and then staff lines. Music notation is, in
  origin, prosody notation that specialized.
- **Tone diacritics** — pinyin's ā á ǎ à and the IPA's Chao tone letters (˥ ˧ ˩) draw pitch
  contours directly into orthography for tonal languages — tiny pitch pictures glued to
  text, used daily by millions of language learners.

**Takeaway:** marks-over-text for melody is ancient, learnable at population scale, and the
ancestor of music notation — but always bound to fixed liturgical melodies or lexical tone,
never free prosody of ordinary speech.

## 2. The elocutionists had this exact idea ~250 years ago

- **Joshua Steele, *Prosodia Rationalis* (1775, 2nd ed. 1779)** — full title: "An Essay
  Towards Establishing the Melody and Measure of Speech, **to be Expressed and Perpetuated
  by Peculiar Symbols**." Steele adapted musical notation to speech, with the key insight
  that spoken pitch *slides* rather than stepping between held tones (he notated slides,
  including celebrated stage delivery of the day, so performances could be preserved and
  reproduced). This is the "anyone could re-create a world-class speech" dream, stated in
  1775. ([Wikipedia](https://en.wikipedia.org/wiki/Prosodia_Rationalis) ·
  [Library of Congress](https://www.loc.gov/item/17006845/) ·
  [full scan on Internet Archive](https://archive.org/details/prosodiarationa01steegoog))
- **John Walker, *The Melody of Speaking Delineated; or, Elocution Taught Like Music, by
  Visible Signs* (1787)** — the title alone is this idea. Walker (the era's leading
  elocutionist and pronouncing-dictionary author) built a system of visible marks for the
  "tones, inflexions, and variations of voice in reading and speaking; with directions for
  modulation, and expressing the passions."
  ([Wikisource](https://en.wikisource.org/wiki/The_Melody_of_Speaking_Delineated) ·
  [Wikipedia on Walker](https://en.wikipedia.org/wiki/John_Walker_(lexicographer)))
- The broader 18th–19th-century **elocution movement** produced many such notations (voice
  and even gesture), then faded with changing fashion — the systems were never unified and
  never survived into common literacy.
- Related in spirit: **Alexander Melville Bell's *Visible Speech* (1867)** — a script
  making *articulation* visible (used to teach deaf students; his son was Alexander Graham
  Bell). Same program of "make the invisible part of speech visible," aimed at phonetics
  rather than prosody. ([Wikipedia](https://en.wikipedia.org/wiki/Visible_Speech))

**Takeaway:** the idea has been independently invented at least twice at book length in the
1700s. It worked well enough to teach from, and still died — mostly of complexity and lack
of an ecosystem (nothing could *play back* a score except a trained human).

## 3. Great orators already hack this privately

- **Winston Churchill's "psalm form"** — Churchill had speeches typed in short, staggered,
  indented lines like free verse so he could see at a glance where to breathe, pause, and
  hit emphasis; he added delivery notes — down to planned hesitations and fake
  self-corrections. ([Imperial War Museums](https://www.iwm.org.uk/history/winston-churchill/what-makes-a-churchill-speech)
  · [International Churchill Society](https://winstonchurchill.org/the-life-of-churchill/life/man-of-words/how-churchill-prepared-for-his-speeches/)
  · [an original "psalm form" draft](https://www.churchillbookcollector.com/pages/books/008734/winston-s-churchill/the-hour-of-our-greatest-effort-is-approaching-an-original-typed-hand-emended-psalm-form-carbon))
- Speechwriters and broadcasters still mark up scripts by hand (underlines for stress,
  slashes for pauses) — private, idiosyncratic, non-standardized.

**Takeaway:** the people who most need prosody-on-paper already invent ad-hoc versions of
it. There is real demand; there has never been a shared standard.

## 4. Linguists built precise notations — for experts only

- **Interlinear "tadpole" transcription** (British tradition; O'Connor & Arnold's
  *Intonation of Colloquial English*, 1961/1973) — syllables drawn as dots (with tails for
  the moving nucleus) placed **between two horizontal lines representing the top and bottom
  of the speaker's pitch range** — literally the "upper wave and lower wave" of this idea,
  in ESL textbooks since the 1960s.
  ([Oxford phonetics overview](https://www.phon.ox.ac.uk/jcoleman/intonation.htm) ·
  [comparison of O'Connor/Arnold and Brazil](https://www.researchgate.net/publication/280737656_English_intonation_models_the_attitudional_approach_of_O'Connor_and_Arnold_and_Brazil's_communicative_approach))
- **Dwight Bolinger** — hundreds of everyday-English examples set "much in the manner of
  musical notation," with print arranged to show pitch movement; he also argued rises and
  falls carry universal, pre-linguistic meaning
  ([review of *Intonation and Its Parts*](https://www.researchgate.net/publication/231820131_review_of_Dwight_Bolinger_1986_Intonation_and_its_parts_melody_in_spoken_English_London_Edward_Arnold_Pp_xiii_421_First_published_1985_Stanford_Ca_Stanford_University_PressAlan_Cruttenden_1986_Intonat) ·
  [D. R. Ladd on intonational universals](https://www.lel.ed.ac.uk/~bob/PAPERS/univs.pdf)).
- **ToBI (Tones and Break Indices, ~1992)** — the shared standard for labeling English
  prosody (pitch-accent labels like H\*, L-L% plus break indices), created so labs could
  share prosodically annotated speech databases; adapted to many languages.
  ([Ohio State guidelines](https://www.ling.ohio-state.edu/research/phonetics/E_ToBI/) ·
  [Wikipedia](https://en.wikipedia.org/wiki/ToBI))
- **Phonetics tooling** — Praat pitch tracks and
  [Prosogram](https://sites.google.com/site/prosogram/home) (stylized pitch contours meant
  to approximate perceived intonation) visualize prosody daily in research.

**Takeaway:** precision exists. ToBI even proves the "shared corpus for machines" half of
the idea. But these notations optimize for analysis, not reading — nobody performs from a
ToBI transcript, and laypeople can't read any of it.

## 5. Teachers and therapists already use the visual trick — because it works

- **Ann Cook, *American Accent Training*** — a mainstream ESL bestseller whose core device
  is **staircase intonation**: sentences drawn as descending staircases, each stressed word
  starting a new staircase; plus a stretched **rubber band** to feel stress physically.
  Mountains-and-waves pedagogy, in print for decades.
  ([book](https://books.google.com/books/about/American_Accent_Training_Book.html?id=9kF-MAEACAAJ) ·
  [staircase explainer](https://strikeenglish.blogspot.com/2013/06/staircase-intonation.html))
- **Visi-Pitch (PENTAX Medical)** — the clinical standard since the 1980s for speech
  therapy: real-time visual traces of pitch, loudness, and timing as biofeedback; shown to
  accelerate therapy goals.
  ([product page](https://www.pentaxmedical.com/pentax/en/98/1/Visi-Pitch-IV-Model-3950B-Computerized-Speech-Lab-CSL-Model-4500-and-4150B) ·
  [RIT on voice tech](https://www.rit.edu/ntid/slpros/instruction/segmental/voice/usingtech))
- **Singing interfaces** — karaoke/rhythm games (SingStar, Rock Band) scroll pitch as bars
  you match; vocal editors (Melodyne-style) show the voice as a piano-roll. People with no
  music training sight-read these instantly.

**Takeaway:** visual pitch/stress feedback demonstrably teaches delivery. All of it is
either drawn diagrams *about* text or plots *beside* text — none of it is a written form
*of* text.

## 6. Designers and HCI researchers: the closest modern matches

This is where the idea is closest to already existing — as research:

- **Prosodic Font** (Tara Rosenberger, MIT Media Lab thesis, 1998) — "the space between
  the spoken and the written": a dynamic font whose forms move with the tonal and rhythmic
  motion of the voice; users could identify prosodic variations from the type alone.
  ([thesis/paper](https://www.researchgate.net/publication/2486426_Prosodic_Font) ·
  [CHI paper "Translating speech into graphics"](https://dl.acm.org/doi/pdf/10.1145/632716.632872))
- **The Kinetic Typography Engine** (Lee, Forlizzi & Hudson, UIST 2002, CMU) — foundational
  system for animating expressive text, ancestor of today's After Effects lyric-video
  culture. ([paper PDF](http://johnnylee.net/kt/dist/files/Kinetic_Typography.pdf))
  Kinetic typography is now everywhere (titles, lyric videos, TikTok captions) — expressive,
  but with **no codified mapping** from voice to motion; each animation is hand-art.
- **Speech-Modulated Typography** (Caluã de Lacerda Pataca & Paula Costa, IUI 2020) — maps
  measured prosody into typography: **loudness → font weight, pitch → baseline shift,
  duration → letter-spacing**. Almost exactly this idea's mapping table.
  ([paper](https://dl.acm.org/doi/10.1145/3377325.3377526) ·
  [author's publications](https://www.caluapataca.com/publications.html))
- **Prosody & emotion in captions for Deaf and hard-of-hearing viewers** (Pataca et al.,
  CHI 2023; follow-ups through CHI 2025) — the same model applied to captions, studied with
  DHH users; accessibility is the live application driving this research.
  ([CHI 2023](https://dl.acm.org/doi/10.1145/3544548.3581511) ·
  [CHI 2025 "Tactile Emotions"](https://dl.acm.org/doi/10.1145/3706598.3713304) ·
  [speech-style captions study](https://www.researchgate.net/publication/384980846_Visualizing_Speech_Styles_in_Captions_for_Deaf_and_Hard-of-Hearing_Viewers))
- Related: [FaceType](https://dl.acm.org/doi/fullHtml/10.1145/3533385) (written impressions
  of spoken expression), and
  [prosodic mapping of font style/size via emotion dimensions](https://link.springer.com/article/10.1186/s13636-016-0087-8)
  (2016).

And the folk versions that already ship at massive scale:

- **Comic lettering** — a working, reader-tested visual prosody code: bigger/bolder letters
  = shouting, burst balloons = screams, wavy/deflated balloons = weak or shaky voice,
  bold-italic = stress. Readers decode it with zero training.
  ([Blambot's grammar of lettering](https://blambot.com/pages/comic-book-grammar-tradition) ·
  [Comicraft glossary](https://balloontales.com/the-comicraft-glossary-of-lettering-terms/))
- **Internet typography** — ALL CAPS = loud, letter stretching = duration ("sooooo"),
  ~tildes~ = sing-song irony, question marks as pitch rises: Gretchen McCulloch documents a
  whole chapter of "typographical tone of voice" conventions in *Because Internet* (2019).
  ([book](https://en.wikipedia.org/wiki/Because_Internet) ·
  [review discussing the chapter](https://languageonthemove.com/because-internet/))
- **Concrete poetry and futurist typography** (Apollinaire's calligrams; Marinetti's
  words-in-freedom using type size for noise and intensity) — the art-historical precedent
  for type as sound.

**Takeaway:** the modern academic version of this idea exists and converges on the same
visual mappings this idea proposes — validation, not invalidation. But it remains
prototypes and papers: no standard notation, no authoring tools, no ecosystem, no
round-trip with TTS.

## 7. Machines already have half the system — the non-visual half

- **SSML** (W3C Speech Synthesis Markup Language 1.0/1.1) — the standard `<prosody>`
  element controls pitch, pitch contour, range, rate, duration, and volume of synthesized
  speech. Codified prosody-in-text exists — as XML nobody can *read*.
  ([W3C spec](https://www.w3.org/TR/speech-synthesis11/))
- **Speech Markdown / SSMD** — community projects wrapping SSML in friendlier author syntax.
  ([speechmarkdown.org](https://speechmarkdown.org/) ·
  [SSMD](https://github.com/machisuji/ssmd))
- **Inline audio tags** (ElevenLabs Eleven v3, 2025) — bracketed performance directions
  like `[whispers]`, `[excited]`, `[pauses]` steer delivery mid-sentence; the industry is
  converging on inline prosody direction, but as *words*, not visual form.
  ([ElevenLabs blog](https://elevenlabs.io/blog/eleven-v3) ·
  [audio tags guide](https://elevenlabs.io/blog/v3-audiotags))
- **Prosody modeling in TTS research** — Global Style Tokens (Wang et al., 2018) learn
  controllable prosodic styles without labels; fine-grained prosody transfer and word-level
  control are active topics, surveyed in the era of LLM-driven TTS. Models can already
  learn and apply prosody; what they lack is a **human-readable interchange notation**.
  ([GST samples](https://google.github.io/tacotron/publications/global_style_tokens/) ·
  [fine-grained prosody transfer](https://arxiv.org/pdf/1907.02479) ·
  [controllable-TTS survey](https://arxiv.org/html/2412.06602v2))
- **Delivery-coaching apps** (Yoodli, Orai, Speeko) — analyze your recorded speech and
  score pacing, pitch/energy, pauses, filler words. They visualize *analytics about* your
  delivery, not a *score of* a delivery someone else could perform.
  ([Yoodli](https://yoodli.ai/use-cases/speech-coaches) · [Orai](https://orai.com/))

**Takeaway:** the machine half of the round-trip (notation → voice) is essentially solved:
a visual notation could compile to SSML/audio tags today, and prosody-labeled paired data is
exactly what expressive-TTS research wants. The missing piece is the human-facing layer.

## 8. The gap — what does *not* exist

| Requirement | Who has it | Who doesn't |
|---|---|---|
| Readable by untrained people | comics, internet typography, staircase diagrams | ToBI, tadpoles, SSML |
| Precise enough to re-perform from | Steele, ToBI, pitch plots | comics, internet typography |
| Lives *in* running text (not beside it) | cantillation, speech-modulated typography | pitch plots, karaoke bars, coaching apps |
| Standardized / shared across users | cantillation, ToBI, SSML | kinetic typography, speechwriters' markups |
| Round-trips with audio (speech ↔ score) | — research fragments only | everyone |
| Adopted beyond a niche | — | everyone |

Closest single precedents: **cantillation** (a lay population reading melody off text — but
fixed liturgical melodies), **Walker 1787** (the concept, pre-technology),
**speech-modulated typography** (the right mapping, still in the lab), and **SSML/audio
tags** (the adoption, in the wrong modality). Nobody occupies the intersection.

## 9. Notes for a future build (if this ever gets picked up)

- **Don't invent mappings from scratch.** The literature and folk practice converge:
  pitch → vertical position/baseline, loudness → size/weight, duration & rate → horizontal
  spacing/stretch, pauses → gaps. These match cross-modal intuitions and tested prototypes;
  a new system should standardize them, not replace them.
- **One source format, two renderers**: static (a printed "score") and kinetic (animated
  captions). The source format is the standard; renderings are interchangeable.
- **Automatic transcription path**: audio → forced alignment + F0/energy/duration
  extraction (Praat-class tooling) → notation. Hand-authoring is for composition;
  auto-scoring is for learning from real performances.
- **Compile path**: notation → SSML `<prosody>` / inline audio tags → any modern TTS =
  instant playback of a score. This also makes every scored text a training pair.
- **Wedge market**: DHH-accessible captions — active research demand, real users, and the
  clearest near-term benefit; speech coaching and ESL prosody teaching are second.
- **The bar for "it works"**: a stranger, given only the score of a famous speech, delivers
  its cadence recognizably — Steele's 1775 goal, finally with a playback device.

## 10. Addendum: the expressive-reader landscape

Added 2026-08-30, after extending the idea to a "prosody engine" that reads any text aloud
with planned, principle-driven delivery (see README). What exists today:

- **Expressive AI readers already ship, at scale.** ElevenLabs'
  [ElevenReader](https://elevenreader.io/) reads articles, PDFs, ePubs and web pages with
  "emotionally rich, context-aware" narration — including licensed, estate-approved
  [Iconic Voices](https://elevenlabs.io/blog/iconic-voices) (Maya Angelou, James Dean, Judy
  Garland, Richard Feynman, Deepak Chopra).
  [Speechify](https://speechify.com/blog/celebrity-voices-with-text-to-speech/) reads any
  webpage/PDF/doc in licensed celebrity voices (Snoop Dogg, Gwyneth Paltrow). So "a famous
  licensed voice reads anything you give it" already exists — the *voice* half of the
  audiobook vision is real.
- **Auto-narrated audiobooks are an industry.** Amazon KDP
  [Virtual Voice](https://kdp.amazon.com/en_US/help/topic/G3QRL9HQNF273Q2H), Apple Books
  digital narration, and Google Play auto-narration mass-produce synthetic audiobooks,
  [distributed across the big five retailers](https://publishdrive.com/ai-narrated-audiobooks-retailers.html).
- **The "LLM director" half-exists as pipelines and research.** LLMs are used to annotate
  text with SSML/prosodic tags before synthesis
  ([ICNLSP 2025 French TTS pipeline](https://github.com/hi-paris/Prosody-Control-French-TTS) ·
  [narrative understanding for expressive TTS](https://arxiv.org/pdf/2509.04072) ·
  [StoryTTS expressiveness-annotated dataset](https://arxiv.org/pdf/2404.14946)), and
  Gemini-class TTS takes
  [inline style tags](https://www.mindstudio.ai/blog/gemini-3-1-flash-tts-controllable-text-to-speech).
- **Teleprompters: manual cues and voice-sync exist; prosody rendering doesn't.**
  Standard prompter practice is hand-marked, coarse cues — bold or colored words and
  [PAUSE] / [SLOW] / [BREATH] tags
  ([Teleprompter.com's markup guidance](https://www.teleprompter.com/blog/writing-effective-speech-scripts-for-teleprompter-apps)) —
  and [PromptSmart's VoiceTrack](https://promptsmart.com/how-it-works) already solves
  speaker-synced scrolling (follows the voice, waits during pauses, resumes on script).
  No product renders continuous visual prosody (melody, volume, rate) on the scroll: the
  two halves exist separately and have never been combined.
- **What still doesn't exist: an exposed delivery plan.** In every shipping system the
  prosody is either inferred end-to-end (opaque; you re-roll, you don't edit) or written as
  markup no listener or reader ever sees. Nobody offers delivery as an explicit,
  principled, *visible and editable* layer — planned the way a trained speaker plans
  (stress, rate, volume, melody varied in parallel, word by word), rendered to the eye as a
  score and to the ear through any licensed voice, with the same score reproducible across
  voices.

The reader/audiobook application therefore confirms the verdict from the machine side:
**production quality exists; control and transparency don't.** The differentiator is not
"expressive voice" (shipped) but "expressiveness you can see, edit, teach, and replay."

## All sources

Historical: [Prosodia Rationalis (Wikipedia)](https://en.wikipedia.org/wiki/Prosodia_Rationalis) · [Steele at Library of Congress](https://www.loc.gov/item/17006845/) · [Steele scan (Internet Archive)](https://archive.org/details/prosodiarationa01steegoog) · [Walker, The Melody of Speaking Delineated (Wikisource)](https://en.wikisource.org/wiki/The_Melody_of_Speaking_Delineated) · [John Walker (Wikipedia)](https://en.wikipedia.org/wiki/John_Walker_(lexicographer)) · [Visible Speech (Wikipedia)](https://en.wikipedia.org/wiki/Visible_Speech) · [Ekphonetic notation (Wikipedia)](https://en.wikipedia.org/wiki/Ekphonetic_notation) · [Hebrew cantillation (Wikipedia)](https://en.wikipedia.org/wiki/Hebrew_cantillation) · [Churchill's speeches (IWM)](https://www.iwm.org.uk/history/winston-churchill/what-makes-a-churchill-speech) · [How Churchill prepared (ICS)](https://winstonchurchill.org/the-life-of-churchill/life/man-of-words/how-churchill-prepared-for-his-speeches/) · [psalm-form draft (Churchill Book Collector)](https://www.churchillbookcollector.com/pages/books/008734/winston-s-churchill/the-hour-of-our-greatest-effort-is-approaching-an-original-typed-hand-emended-psalm-form-carbon)

Linguistics & pedagogy: [ToBI guidelines (OSU)](https://www.ling.ohio-state.edu/research/phonetics/E_ToBI/) · [ToBI (Wikipedia)](https://en.wikipedia.org/wiki/ToBI) · [Intonation overview (Oxford)](https://www.phon.ox.ac.uk/jcoleman/intonation.htm) · [O'Connor & Arnold vs Brazil (ResearchGate)](https://www.researchgate.net/publication/280737656_English_intonation_models_the_attitudional_approach_of_O'Connor_and_Arnold_and_Brazil's_communicative_approach) · [Bolinger review (ResearchGate)](https://www.researchgate.net/publication/231820131_review_of_Dwight_Bolinger_1986_Intonation_and_its_parts_melody_in_spoken_English_London_Edward_Arnold_Pp_xiii_421_First_published_1985_Stanford_Ca_Stanford_University_PressAlan_Cruttenden_1986_Intonat) · [Ladd, intonational universals](https://www.lel.ed.ac.uk/~bob/PAPERS/univs.pdf) · [Prosogram](https://sites.google.com/site/prosogram/home) · [American Accent Training (Google Books)](https://books.google.com/books/about/American_Accent_Training_Book.html?id=9kF-MAEACAAJ) · [staircase intonation](https://strikeenglish.blogspot.com/2013/06/staircase-intonation.html) · [Visi-Pitch (PENTAX)](https://www.pentaxmedical.com/pentax/en/98/1/Visi-Pitch-IV-Model-3950B-Computerized-Speech-Lab-CSL-Model-4500-and-4150B)

HCI & design: [Prosodic Font (ResearchGate)](https://www.researchgate.net/publication/2486426_Prosodic_Font) · [Prosodic Font (ACM)](https://dl.acm.org/doi/pdf/10.1145/632716.632872) · [Kinetic Typography Engine (PDF)](http://johnnylee.net/kt/dist/files/Kinetic_Typography.pdf) · [Speech-modulated typography (ACM IUI 2020)](https://dl.acm.org/doi/10.1145/3377325.3377526) · [Prosody & emotion captions (CHI 2023)](https://dl.acm.org/doi/10.1145/3544548.3581511) · [Tactile Emotions (CHI 2025)](https://dl.acm.org/doi/10.1145/3706598.3713304) · [Speech-style captions](https://www.researchgate.net/publication/384980846_Visualizing_Speech_Styles_in_Captions_for_Deaf_and_Hard-of-Hearing_Viewers) · [FaceType (ACM)](https://dl.acm.org/doi/fullHtml/10.1145/3533385) · [Prosodic font mapping via emotion dimensions (Springer)](https://link.springer.com/article/10.1186/s13636-016-0087-8) · [Pataca publications](https://www.caluapataca.com/publications.html) · [Blambot lettering grammar](https://blambot.com/pages/comic-book-grammar-tradition) · [Comicraft glossary](https://balloontales.com/the-comicraft-glossary-of-lettering-terms/) · [Because Internet (Wikipedia)](https://en.wikipedia.org/wiki/Because_Internet) · [Because Internet review](https://languageonthemove.com/because-internet/)

Machine side: [SSML 1.1 (W3C)](https://www.w3.org/TR/speech-synthesis11/) · [Speech Markdown](https://speechmarkdown.org/) · [SSMD (GitHub)](https://github.com/machisuji/ssmd) · [Eleven v3](https://elevenlabs.io/blog/eleven-v3) · [Eleven v3 audio tags](https://elevenlabs.io/blog/v3-audiotags) · [Global Style Tokens samples](https://google.github.io/tacotron/publications/global_style_tokens/) · [Fine-grained prosody transfer (arXiv)](https://arxiv.org/pdf/1907.02479) · [Controllable TTS survey (arXiv)](https://arxiv.org/html/2412.06602v2) · [Yoodli](https://yoodli.ai/use-cases/speech-coaches) · [Orai](https://orai.com/)

Origin of the spark: [Stage Academy by Vinh Giang](https://vinhgiang.com/programs/stage-academy) — its early Vocal Foundations / Vocal Mastery modules teach the voice as an instrument (rate of speech, volume, pitch, projection). Similar framings exist elsewhere, e.g. [Julian Treasure's "vocal toolbox"](https://www.speeko.co/blog/summary-ted-talk-julian-treasure-how-to-speak).
