---
name: cine-director
description: >-
  Use when the user gives a short creative brief (plus optional reference images —
  person, product, wardrobe, scenario, vehicle) and wants a complete director-level
  video-generation prompt for a single continuous ~20s multi-shot film, ANY segment
  (commercial, editorial, fashion, automotive, food, real estate, tech, corporate,
  beauty, travel, etc.), ANY AI video model. Asks which platform the prompt
  targets, then acts as director + cinematographer + production designer +
  screenwriter to lock shots, camera moves, drone use, lighting, narrative,
  transitions, SFX and optional VFX, anchored to the segment's top-brand visual
  codes, locked against hallucination and consistency drift. Generalist
  master-prompt skill — for food/wearable-fashion/fitness/talking-head niches,
  prefer food-ad, lookbook-ad, workout-hype, motion-hack or kinetic-multicam
  instead. PT: "quero um prompt de vídeo cinematográfico pra minha marca", "cria a
  direção completa desse comercial", "gera o prompt master desse vídeo".
---

# cine-director: brief → master cinematic prompt (any segment, any AI)

## Overview

Turns a short creative brief — plus whatever reference images exist (person,
product, wardrobe, scenario/location, vehicle) — into ONE complete, ready-to-paste
video-generation prompt for a **single continuous ~20s film with multiple shots,
framings and camera moves** (not a slideshow of disconnected clips). You act as the
full crew on this: **director, director of photography, production designer,
screenwriter, camera operator.** The goal, every time, is a spot that reads like it
came out of the top production house in whatever segment the brief describes —
never a generic AI-video look.

**Core principle: lock everything down so the model cannot drift or invent.**
Identity (face, product design, wardrobe, location, vehicle, brand colors/logo) is
anchored to the reference images and stated **once, explicitly, as a consistency
lock** that every shot must obey. Anything not sourced from a reference or confirmed
by the user (on-screen text, logos, taglines, claims) is never invented — it is
either omitted, asked about, or written as a qualitative visual description, never a
fabricated fact.

**REQUIRED reading before filling anything:**
- `references/segment-library.md` — shot/lighting/pacing/SFX conventions per
  segment (automotive, fashion, tech, real estate, beauty, corporate, travel...) plus
  a universal method for deriving conventions for a segment not listed.
- `references/platform-conventions.md` — how to format the final prompt for the
  target AI (Seedance-style JSON, Veo/Omni/Kling/Runway/Sora-style prose, or a
  portable generic format).

---

## Workflow

### Step 0 — Ask the target platform (mandatory, first question)

Prompt syntax differs a lot by model. Before anything else, ask (bundled with Step 1
if possible): **"Qual IA/plataforma vai gerar esse vídeo?"** (Seedance 2.0, Google
Veo / Omni Flash, Kling, Runway, Sora, Luma, Pika, or "não sei / me dá algo
universal"). Read `references/platform-conventions.md` and use that platform's
conventions for the final prompt. If the user doesn't know, default to the portable
generic format and say so.

### Step 1 — Collect the brief (one bundled question, only for what's missing)

Need:
- **Central idea** — the user's short text. This drives everything else.
- **Segment/category** — infer it from the idea when possible (a car launch reads as
  automotive, a skincare close-up reads as beauty); confirm out loud, only ask if
  genuinely ambiguous.
- **Reference images available** — ask which of these exist and to attach them:
  **person**, **product**, **wardrobe**, **scenario/location**, **vehicle**. None are
  mandatory — the skill can generate 100% from text, but flag which elements are
  therefore "art-directed from the brief" rather than identity-locked to a photo.
- **Duration** — default **20 seconds** (this skill's sweet spot for a single
  multi-shot continuous film); allow override.
- **Aspect ratio** — default 9:16 (social) unless the brief implies otherwise (a
  cinema-style commercial reads 16:9); ask if unclear.
- **VFX** — ask explicitly: "Quer VFX conceitual (partículas, luz, atmosfera), sem
  pesar a imagem, ou prefere sem VFX?" Default OFF / minimal if unanswered.

Never ask about music — **audio is SFX-only by default, no soundtrack**, per the
hard rules below. Only add music if the user explicitly asks for it.

### Step 2 — Research the segment

Read `references/segment-library.md`.
- If the segment is **cataloged**, pull its shot/lighting/pacing/SFX profile and its
  noted variations.
- If it's **not cataloged**, derive one from the library's **universal beat
  taxonomy** (hook → establish/introduce → core action/demo → hero detail →
  climax/reveal → closing brand frame) and the **universal camera/lighting
  vocabulary**.
- Use WebSearch to ground the profile in real conventions of 2-3 leading brands in
  that exact segment — their typical shot grammar, lighting signature, pacing,
  iconic camera moves, color grade. This is about **visual language, not factual
  claims** — never invent a brand's specific tagline, number, or logo unless the
  user supplies it or it's common public knowledge you can verify.
- If reference images exist, note their real observed traits (read the images —
  never guess unseen details) for the consistency lock in Step 4.
- Decide, for THIS brief: does a **drone/aerial shot** actually fit? It belongs in
  automotive, real estate, travel/landscape, outdoor sports/lifestyle — it does NOT
  belong forced into an intimate interior, a beauty macro, or a tabletop product
  shot. Never add a drone shot just because the format allows one.

### Step 3 — Build the shot list (MANDATORY checkpoint before writing the prompt)

Break the chosen duration into **4–6 beats**, sized so each can breathe (roughly
3–5s each for a 20s film). For each beat, decide:

- **Time range** (e.g. `0-3s`)
- **Shot type / framing** (wide establishing, medium, hero close-up, macro detail,
  over-the-shoulder, POV...)
- **Camera movement** (static, dolly, tracking, crane, orbit, whip-pan, push-in,
  pull-out, handheld, drone flyover/reveal — only if it earned its place in Step 2)
- **Lens** (wide 24mm for scale/action, 50-85mm for people, 100mm macro for texture)
- **Lighting note** (consistent with the segment's lighting recipe from Step 2)
- **Narrative beat** — what this shot is doing for the story (hook, tension, payoff…)
- **Transition in** (hard cut, whip-pan, match cut, morph, speed ramp — named, never
  left generic)
- **SFX cue** for this beat
- **VFX cue** for this beat, only if the user opted in — kept conceptual and light
  (a single atmospheric or particle effect per beat at most, never stacked)

Present this as a clear table **before writing the final prompt** and ask the user
to accept it or adjust: block count/timing, any shot, the drone call, the VFX
intensity, the SFX list. **Never skip this checkpoint** — it's what keeps the final
prompt aligned with what the user actually pictured, and it's the same checkpoint
pattern that prevents wasted generations across every skill in this family.

### Step 4 — Write the consistency lock (this is what stops hallucination)

Before the shot-by-shot prompt, write one explicit block that must hold across
**every single beat**:

- **Identity:** for each reference supplied (person / product / wardrobe /
  scenario / vehicle), state its real observed traits in one line each, tagged to
  its reference placeholder (see below). Nothing invented — only what the image or
  the user's brief actually established.
- **Never-change list:** face, body proportions and expression range (person);
  exact product design, materials, proportions, and any visible branding (product);
  garments and how they're worn (wardrobe); architecture, palette and key set
  dressing (scenario); make/model/color/plate-visibility rules (vehicle).
- **On-screen text/logo lock:** if any text, logo or wordmark appears, list the
  EXACT allowed strings — nothing else may render as text anywhere in the video.
  If there is no on-screen text, say so explicitly ("no on-screen text anywhere").
- **Reference placeholders:** tag each supplied image `<<<image_person>>>`,
  `<<<image_product>>>`, `<<<image_wardrobe>>>`, `<<<image_scenario>>>`,
  `<<<image_vehicle>>>` (only include the tags that apply) — each carrying `no grid
  lines, no overlay, no mesh` to stop reference-artifact leakage, matching the
  convention in `references/platform-conventions.md`.

### Step 5 — Generate the master prompt

Read `references/platform-conventions.md` and format for the confirmed target
platform. Every version — JSON or prose — must contain, in this order:

1. Duration + aspect ratio.
2. The consistency lock from Step 4 (identity, never-change list, text/logo lock,
   reference tags).
3. Segment-appropriate style/lighting recipe (from Step 2), stated once as the
   through-line, not repeated differently per shot.
4. The confirmed shot list from Step 3, shot-by-shot: time range, framing, camera
   movement + lens, transition in, brief narrative/action line, SFX cue, VFX cue
   (only if opted in).
5. **Audio block:** `music: NO background music, no soundtrack, no score` (unless
   the user explicitly asked for music) + the full SFX list, diegetic and matched
   to the actual actions in the video.
6. If the target platform generates short clips (check
   `references/platform-conventions.md` for known per-model caps), a one-line note
   telling the user how the 20s splits into N clips to generate and stitch, sized so
   the cuts land on beat boundaries — never mid-beat.

### Step 6 — Deliver

1. The prompt in a copyable code block, formatted for the chosen platform.
2. A short setup line: which reference image goes in which slot, suggested
   generation settings (duration, aspect ratio), and — if applicable — the
   clip-splitting note from Step 5.
3. Save `<project name or idea slug> - cine-director prompt.md` in the session
   folder: brief, segment research + sources, confirmed shot list, consistency
   lock, and the final prompt.

---

## Hard rules (never break these)

- **Always ask the target platform first** (Step 0) — the prompt's format depends
  on it.
- **Never skip the Step 3 shot-list checkpoint.** Delivering an unconfirmed shot
  list is the #1 way this skill wastes a generation.
- **Never default to background music.** SFX only, unless explicitly requested.
- **Never invent on-screen text, logos, taglines, numbers, or claims.** If it's not
  in a reference image, the brief, or verified research, it doesn't go in the
  prompt — ask instead.
- **Never force a drone/aerial shot into a segment where it doesn't belong.** Match
  it to the scene logic (Step 2), not to "it looks cool."
- **Never stack VFX.** Conceptual and restrained — one effect per beat at most, and
  only if the user opted in.
- **Never drop the consistency lock** from the final prompt — it's the whole reason
  the video won't drift between shots.
- **Never write a single-shot, static prompt when the brief calls for a film.** This
  skill's output is always multi-beat, multi-camera, one continuous piece.

## Do NOT (observed failure modes this skill exists to prevent)

- Do NOT guess a segment's visual codes from a stereotype — ground them in Step 2
  research, and say so honestly if research came up thin (fall back to the
  universal taxonomy, don't fabricate "Ferrari does X" without a source).
- Do NOT let reference images go unread — traits in the consistency lock must come
  from actually looking at the image, never assumed.
- Do NOT write vague transitions ("cut to next shot"). Every transition is named
  and intentional.
- Do NOT let beat count run away — more than 6 beats in 20s reads as frantic, not
  cinematic; fewer than 4 reads as a single ad still, not a film.
- Do NOT overwrite this skill's territory onto the specialized ones — if the brief
  is squarely a food hero-shot video, a fashion lookbook, a talking-head reel, or a
  gym hype video, say so and point to the matching specialist skill (food-ad,
  lookbook-ad, kinetic-multicam/motion-hack, workout-hype) instead, since they
  encode more niche-specific detail than the generalist path here.
- Do NOT deliver before the Step 3 checkpoint is answered.
