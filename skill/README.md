# Skills

This folder bundles Claude Code skills designed to work alongside the storyboard workflow.

## `video-prompt-builder/`

A Claude Code skill that turns a creative brief into a structured, shot-by-shot Seedance 2.0 prompt. It enforces six hard rules learned from production:

1. **Generation strategy gate** — always asks whether you want one long multi-shot Seedance gen or several stitched gens.
2. **Real people require real photos** — never hallucinates a portrait of a real person.
3. **VO word-distribution** — keeps speech speed consistent across stitched gens.
4. **Cost preflight** — declares Higgsfield Ultra credit estimate before locking shot count.
5. **Image model routing** — defaults to GPT Image 2 for characters, Nano Banana Pro for off-state lighting, never silently swaps models.
6. **Default architecture** — real-photo ref + structured shot list + b-roll cutaways + VO-synced timing.

## How to install

### Option A — Per-user (recommended)

Copy the skill into your Claude Code skills directory:

```bash
cp -R skill/video-prompt-builder ~/.claude/skills/
```

Claude Code will pick it up on next launch. The skill triggers on any brief that mentions video prompts, Seedance, shot lists, ad concepts, brand films, or storyboards.

### Option B — Project-scoped

Leave it in `skill/` and reference it from your project's `CLAUDE.md` as a local skill location.

## How to use it

Once installed, just describe what you want:

> "Write me a 20-second brand film for a coffee subscription. Mountain setting, golden hour, generic mug. Multi-shot Seedance."

The skill will ask the Rule 1 gate question, walk through the hard rules, then produce the four-section output (timeline, effects inventory, density map, energy arc).
