# cine-director

**Type a sentence. Get a Hollywood-grade shot list.**

`cine-director` turns one short creative brief — plus whatever reference photos you have (a person, a product, an outfit, a location, a car) — into a complete, professional, director-level video-generation prompt. Not a caption. Not a vibe. A full **~20-second, multi-shot, single continuous film**, blocked out shot-by-shot exactly like a real production would brief it: framing, lens, camera move, drone call, lighting, narrative beat, transition, SFX — locked hard so the AI can't drift, hallucinate a logo, or forget what your product looks like halfway through the video.

It works for **any segment** — automotive, fashion, tech, real estate, beauty, food, corporate, travel, or whatever you throw at it — and **any AI video model**. It asks which one you're generating on and writes the prompt in that platform's dialect.

> You bring the idea. It brings the entire crew: director, cinematographer, production designer, screenwriter, camera operator — all reasoning about your specific brief like they're pitching to the biggest brand in that category.

---

## Why this isn't just "another prompt generator"

Most AI video prompts are one flat paragraph and a prayer. That's why the outputs look cheap: no shot logic, no lighting continuity, no reason for the camera to move where it moves — and the second the model has to hold a face or a product across multiple beats, it drifts.

`cine-director` is built the opposite way:

- **It thinks like the segment's top brands, not like a stock template.** It researches the actual visual codes of 2–3 leading players in your exact category before writing a single shot — low-angle tracking + chiaroscuro for automotive, macro texture + high-key soft light for tech, golden-hour drone reveals for travel and real estate. The look is earned, not guessed.
- **It locks identity so nothing drifts.** Every reference image you supply gets read for its real traits and welded into a non-negotiable "consistency lock" that every single shot must obey — face, product design, wardrobe, set, vehicle, and exactly which words (if any) are allowed to appear as on-screen text. No invented specs, no morphing face, no logo that changes between beats.
- **It never skips the check.** Before writing the final prompt, it shows you the full shot list — every beat, every camera move, every transition — and waits for your OK. You catch a bad call before you burn a generation on it, not after.
- **It's segment-agnostic by design.** One skill, every category. A universal beat taxonomy and camera/lighting vocabulary mean it can build a credible shot list for a segment that isn't even in its library yet.
- **It targets YOUR platform.** Seedance-style JSON, Veo/Omni Flash prose, Kling, Runway, Sora — it asks first, then writes in that model's native dialect instead of a generic paragraph that half-works everywhere.
- **SFX, never stock music.** Every transition and beat gets diegetic sound design matched to what's actually happening on screen. Music only if you explicitly ask.
- **VFX on your terms.** Conceptual, restrained, opt-in — never a cluttered mess of stacked effects.

## What you get, in one message

1. A **shot list** — 4 to 6 beats, timed, framed, lit, and justified — for you to approve or tweak.
2. A **consistency lock** — the non-negotiable identity/brand rules every shot must follow.
3. The **final master prompt**, formatted for your target AI, ready to paste.
4. A saved `.md` file with your brief, the research sources, the shot list, and the prompt — so nothing is lost if you walk away mid-session.

## How it works

```
you: a short idea + (optional) reference images — person, product, wardrobe, scenario, car
      ↓
skill asks: which AI is this for? (Seedance / Veo-Omni / Kling / Runway / Sora / "surprise me")
      ↓
skill researches the segment's top-brand visual codes (camera, light, pacing, SFX)
      ↓
skill proposes a full shot list — you approve or adjust (mandatory checkpoint)
      ↓
skill writes the consistency lock + the master prompt in your platform's format
      ↓
you paste it into your generator → one continuous, multi-shot, on-brand film
```

## Example

**Input:** *"Lançamento de um relógio esportivo de luxo, clima urbano à noite, close no mecanismo."*

**Output (abridged):** a segment profile pulling from luxury-watch and automotive-adjacent visual codes (chiaroscuro, hard specular hits, slow macro orbit on the mechanism) → a 5-beat shot list (hook macro on the crown → establishing wide of the city at night → hero close-up on the wrist → macro on the moving gears → closing static hero frame) → a consistency lock pinning the watch's exact case shape, dial layout and strap material across every beat → a complete Seedance-JSON (or Veo prose) prompt with diegetic SFX (mechanism ticks, fabric, city ambience) and zero background music.

## Structure

```
cine-director/
├── SKILL.md                          # the workflow, hard rules, consistency-lock method
└── references/
    ├── segment-library.md            # shot/light/pacing/SFX conventions per segment + universal method
    └── platform-conventions.md       # how to format the prompt per target AI model
```

## Install

Clone into your Claude Code skills directory:

```bash
git clone https://github.com/renatoreissc/cine-director.git ~/.claude/skills/cine-director
```

Windows (PowerShell):

```powershell
git clone https://github.com/renatoreissc/cine-director.git "$env:USERPROFILE\.claude\skills\cine-director"
```

Then just describe the film you want — no slash command required, though `/cine-director` works too.

## No scripts, no dependencies

Pure prompt-engineering skill — two reference files and a workflow. No Python, no API keys, nothing to install beyond the skill itself.

## License

MIT. See `LICENSE`.
