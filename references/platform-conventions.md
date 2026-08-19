# Platform Conventions — cine-director

How to format the final prompt once the target platform is known (SKILL.md Step 0).
The **content** (consistency lock, segment style, shot list, audio) is always the
same — only the **syntax** changes. If the user doesn't know their target platform,
use the **Generic / portable** format at the end.

---

## Seedance 2.0 (and similar structured-JSON video models)

- Format as a single JSON object. Suggested keys: `scene_duration`,
  `consistency_lock`, `references`, `style` (environment/lighting/effects),
  `camera_language` (general + lenses), `audio` (music/sound), `sequence` (array of
  beats, each with `time`, `shot`, `camera`, `transition`, `sfx`, `vfx`).
- Reference placeholders: `<<<image_person>>>`, `<<<image_product>>>`, etc. Each
  carries `no grid lines, no overlay, no mesh` inline in its description to prevent
  the reference sheet's own artifacts leaking into the render.
- These models tend to generate short clips (often ~5s per generation) — if the
  chosen duration exceeds that, split the `sequence` into clip-sized chunks on beat
  boundaries and tell the user how many clips to generate and stitch.
- Keep numeric fields (speed ramps, time ranges) precise; keep everything else
  descriptive language, not engineering specs (no pixel/opacity/degree numbers).

## Google Veo / Omni Flash

- Format as flowing natural-language paragraphs, not JSON. Open with the
  consistency lock as a short paragraph ("Preserve X, Y, Z exactly as shown..."),
  then describe the film as a continuous camera-and-narrative passage, beat by beat,
  using time cues in prose ("From 0 to 3 seconds, ... then the camera ...").
- Reference images are attached directly (no bracket-tag convention needed) — refer
  to them in prose as "the attached reference" or "@image1/@image2" if the target
  tool uses that convention; state clearly which reference maps to which role
  (person / product / wardrobe / scenario / vehicle).
- Omni Flash responds well to explicit "do not replace/redesign/hallucinate the
  scene" language for identity-preservation tasks (video-to-video) — include a
  version of that line when a real source video/photo is being preserved rather than
  generated from scratch.
- Strong at continuous camera movement described in prose; lean on that rather than
  cut-heavy language when the brief wants a single unbroken take feel.

## Kling

- Prose-based, similar register to Veo/Omni, but responds well to explicit motion
  **strength** descriptors (subtle / moderate / strong) alongside the movement name
  — state both, e.g. "a strong, fast dolly-in" vs. "a subtle, slow dolly-in."
- Keep each beat's action description tight and unambiguous — Kling can drift on
  long, multi-clause action lines. Prefer short, sequential sentences per beat over
  one long paragraph.

## Runway (Gen-4 and similar)

- Prose plus explicit camera-control phrasing — Runway responds well to naming the
  exact camera move (dolly in / orbit left / static / pan right) as a discrete
  instruction near the start of each beat's description, rather than buried mid
  sentence.
- If the target supports keyframe/reference-image anchoring per shot, note which
  reference image anchors which beat.

## Sora

- Rich narrative prose — Sora handles longer, more novelistic scene descriptions
  and physical coherence well. Lean into narrative connective tissue between beats
  (why the camera moves, what just happened) rather than a terse shot list — but
  still keep the consistency lock and shot list structure underneath so nothing
  drifts.

## Generic / portable (default when the platform is unknown)

Use natural-language paragraphs, structured with clear headers so it can be
adapted to whatever tool the user ends up using:

```
DURATION & FORMAT: <duration>, <aspect ratio>

CONSISTENCY LOCK:
<identity/never-change list/on-screen text lock, one line per element>

REFERENCES:
<image slot> = <role> — <observed traits, no grid lines/overlay/mesh>

STYLE:
<segment lighting/style recipe, stated once>

SHOT LIST:
[0-3s] <framing> — <camera move + lens> — <transition in> — <action/narrative
beat> — SFX: <cue> — VFX: <cue or "none">
... (repeat per beat)

AUDIO:
Music: NO background music, no soundtrack, no score (unless requested).
Sound: <full diegetic SFX list>
```

This format carries cleanly into almost any current text-to-video or
image/video-to-video tool, and is the safe fallback whenever the user says "não sei"
or wants something they can try on more than one platform.
