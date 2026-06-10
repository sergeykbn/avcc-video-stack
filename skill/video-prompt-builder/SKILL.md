---
name: video-prompt-builder
description: Generate detailed, shot-by-shot AI video prompts for Seedance 2.0 from a creative brief. Use this skill whenever the user wants to create a video prompt, write a shot list, plan a video sequence, describe a video concept for AI generation, or mentions Seedance. Also trigger when the user describes a scene, ad concept, brand film, product video, or any visual sequence they want turned into structured prompts — even if they don't explicitly say "video prompt." Trigger on phrases like "write me a video prompt", "Seedance prompt", "shot list", "plan a video", "video concept", "create a sequence", "brand film prompt", "ad prompt", or any time the user describes what they want to happen in a video and needs it translated into generation-ready prompts.
---

# Video Prompt Builder for Seedance 2.0

Build cinematic, shot-by-shot video prompts from a creative brief. Every output follows a structured effects breakdown format designed to give Seedance 2.0 maximum detail on camera work, effects, transitions, pacing, and energy arc.

Before writing prompts, this skill enforces a set of non-negotiable rules learned the hard way across production. Skipping them produces broken cuts, wasted credits, or unusable footage.

## STEP 0 — HARD RULES (run before writing anything)

These rules are mandatory. Walk through each one before producing the 4-section output. If a rule is violated by the brief, pause and resolve it before continuing.

### Rule 1: Generation strategy gate — ALWAYS ASK FIRST

Before writing any prompt, ask the user this exact question:

> Do you want me to write this as **(A) one long Seedance 2 multi-shot generation** containing all shots in a single prompt, or **(B) multiple separate generations** (one per shot or per shot-pair) that you'll stitch together later?

This changes the entire prompt structure downstream:

- **(A) Multi-shot single gen** — write ONE prompt with all shots joined by explicit beat markers and in-prompt transitions. One total duration. Continuity (lighting, character, palette) is enforced by the single render, not by stitching. Best for 5–15 sec pieces with strong continuity needs.
- **(B) Stitched separate gens** — write ONE prompt PER shot (or per first-frame/last-frame pair). Each prompt includes explicit anchor language (`first-frame.png`, `last-frame.png`) and continuity locks (same character, same palette, same wardrobe). Best for 15+ sec pieces, dense edits, or anything needing approval gates per shot.

Do not assume. Even if the brief implies one or the other, confirm explicitly. Adapt section structure to the chosen path.

### Rule 2: Real people require real photos

If the brief features a specific real person (named, recognisable, or "the user themselves"), STOP. Do not generate or describe a "[Name]-like" portrait. Ask the user to attach a real photo to use as image reference for storyboard frames. Generic characters ("a runner", "a barista", "a chef") are fine to describe in prose.

### Rule 3: VO word-distribution (if voiceover is in the brief)

When the video has VO and will be split across multiple equal-duration generations:

- Word count per generation MUST be proportional to that gen's duration.
- Two 5-second gens → each gets exactly half the VO words. Three 5-second gens → equal thirds.
- Imbalance produces visibly different speech speed across cuts and reads as broken.
- If shot durations are unequal, calculate and document target words-per-second per gen.

State the word distribution explicitly in the prompt or in a sidebar note.

### Rule 4: Cost preflight (Higgsfield Ultra)

Before locking shot count, declare estimated credit cost:

- **Seedance 2.0**: ~23 credits per 5s / 720p generation
- **Soul** (portraits): free on Ultra
- **Concurrency cap**: 8 simultaneous jobs on Ultra — batch shots in serial waves of ≤8

If total estimate exceeds ~200 credits, surface the number before committing to the shot count. Offer a reduced-shot alternative.

### Rule 5: Image model routing for storyboard frames

When the prompt also requires storyboard image generation, default to:

- **Portraits / characters / hero shots** → GPT Image 2 (high, 2k)
- **Off-state objects, contradictory lighting, dark/broken states** → Nano Banana Pro (Soul's prompt enhancer overrides "lights off / different lighting" instructions when a ref photo is attached)
- **Soul 2.0** is deprioritised — outputs rated poor for character work
- **Never silently swap models.** If the chosen model lacks a needed parameter (aspect ratio, ref-image slot, lighting control), ASK the user before substituting. Model choice is part of the brief, not an implementation detail.

### Rule 6: Default architecture (the winning formula)

Use this as the baseline unless the user overrides:

- Real-photo image reference where a real person is involved
- Structured shot list using this skill's 4-section output
- Generation strategy chosen via Rule 1
- B-roll cutaways inserted between hero beats
- Cutaway timing synced to VO beats (when VO exists), not placed arbitrarily

## How this skill works

1. The user provides a **creative brief** — can be one line ("a runner in a stadium for a Nike-style ad") or a full storyboard description. They may also include a reference video, mood, brand context, or specific effects.
2. Walk through STEP 0 hard rules. Ask the Rule 1 gate question. Resolve any conflicts (real-people photos, IP language, cost ceiling).
3. Read the reference file at `references/effects-breakdown-reference.txt` to internalise the structure and level of detail expected.
4. Generate the full four-section output, adapted to the chosen generation strategy.

## Input expectations

The brief can include any combination of:

- Subject/talent description (who or what is on screen)
- Setting/environment
- Mood, tone, energy level
- Brand or product context
- Specific effects or camera moves
- Duration target
- Reference to existing ads, films, or visual styles
- Colour palette or grade preferences
- Voiceover script and per-shot timing

If the brief is too vague to build a full prompt, ask one focused clarifying question before proceeding. Do not over-interrogate — work with what you're given and make creative decisions where the user hasn't specified, then surface those decisions for review.

## Output structure

ALWAYS output ALL FOUR sections in this exact order. Never skip a section. Adapt content based on the Rule 1 strategy:

- If **single multi-shot gen** → Section 1 is one continuous prompt with shot beats; Sections 2–4 describe the unified piece.
- If **stitched separate gens** → Section 1 is one block per shot, each ready to paste into Seedance independently.

### Section 1: SHOT-BY-SHOT EFFECTS TIMELINE

Each shot gets its own block structured like this:

```
SHOT [N] ([timestamp]) — [Shot Name / Description]
• EFFECT: [Primary effect name] + [secondary effects if stacked]
• [Detailed description of what's happening visually]
• [Camera behaviour — angle, movement, lens if relevant]
• [Speed/timing information]
• [How this shot connects to the next — transition type]
```

Guidelines:

- Each shot 1–4 seconds unless the brief calls for longer holds
- Name effects precisely: "speed ramp (deceleration)" not "speed ramp"; "digital zoom (scale-in)" not "zoom"
- List all stacked effects explicitly
- Include transition logic: how this shot EXITS and how the next ENTERS
- Use language Seedance 2.0 can interpret — describe the visual result, not the editing technique. "The frame scales inward rapidly", not "apply a keyframed scale effect in After Effects"
- Mark the signature shot: `This is the SIGNATURE VISUAL EFFECT`
- Be specific about speed percentages for slow-motion (e.g., "approximately 20–25% speed")
- Describe motion blur, light behaviour, atmospheric effects when relevant

### Section 2: MASTER EFFECTS INVENTORY

A numbered list of every distinct effect used, with:

- Effect name
- Usage count (e.g., "used 3x")
- Which shots it appears in
- One-line description of its role

Group by category: speed manipulation, camera movement, digital effects, transitions, compositing, optical effects.

### Section 3: EFFECTS DENSITY MAP

Break the timeline into 3–6 second segments and rate each:

- **HIGH DENSITY** — 4+ effects stacked or rapid-fire
- **MEDIUM DENSITY** — 2–3 effects
- **LOW DENSITY** — 1 effect or clean footage

Format:
```
[timestamp range] = [DENSITY LEVEL] ([brief effect list] — [count] effects in [duration])
```

### Section 4: ENERGY ARC

Describe the energy structure as a narrative arc:

- **Act 1**: Opening — how it grabs attention
- **Act 2**: Middle — how it develops, signature moments
- **Act 3**: Resolution — how the energy lands

Adapt act count to length. A 5-second clip might need two beats; a 30-second brand film might need four.

## Creative principles

1. **Contrast drives impact.** Alternate high-density and low-density moments. A slow-motion shot after a speed ramp hits harder than two ramps back-to-back.
2. **Signature moments matter.** Every video needs at least one "hero" effect — something visually distinctive that makes it memorable. Call it out explicitly.
3. **Transitions are shots.** Don't treat transitions as throwaway connectors. A whip pan, a bloom flash, a motion blur smear — creative moments, not just cuts.
4. **Specificity over vagueness.** "The frame rotates clockwise by approximately 15–20°" beats "the camera tilts." "Approximately 20–25% speed" beats "slow motion."
5. **Energy must resolve.** No matter how intense the opening, the video has to land. The final moments should feel intentional.

## Tone and style

- Direct, technical tone — like director's shot notes, not a marketing brief
- Bullet points within each shot block
- Concise but complete — every detail earns its place
- No hype language ("stunning", "breathtaking") — describe what happens, let visuals speak

## Duration calibration

- **5–10 seconds**: 4–7 shots, lean and punchy, 1 signature effect
- **10–20 seconds**: 8–14 shots, room for contrast and build, 1–2 signature effects
- **20–30 seconds**: 12–20 shots, full three-act arc, 2–3 signature effects
- **30+ seconds**: scale accordingly, maintain density contrast — don't fill every second with effects

If duration isn't specified, default to 15–20 seconds (sweet spot for AI video generation).

## Example workflow

**User says:** "I want a dramatic brand film for a trail running shoe. Mountain setting, golden hour, single runner. Make it feel epic but not over-the-top. About 15 seconds."

**You do:**

1. **Rule 1 gate** — ask: "One long 15-second multi-shot Seedance gen, or stitched separate gens?"
2. **Rule 2** — is the runner a real person? If yes, ask for their photo. If generic, proceed.
3. **Rule 4** — cost preflight. 15s = ~3 × 5s gens = ~70 credits (if stitched). State this.
4. Read `references/effects-breakdown-reference.txt` to calibrate detail level.
5. Generate the full four-section output adapted to the chosen strategy.
6. Present in plain text in chat.
