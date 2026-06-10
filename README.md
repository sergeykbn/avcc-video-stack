# AVCC Video Stack

A complete workflow for building AI-generated short-form video, ad-by-ad. Folder system, hard-rule skill, and a clickable demo — everything you need to ship a 15–30 second reel without losing your mind.

## What's inside

```
avcc-video-stack/
├── skill/
│   └── video-prompt-builder/     # Claude Code skill (6 hard rules for Seedance 2.0)
├── projects/
│   ├── demo-avcc-workshop/       # Clickable example — finished 30s AVCC workshop ad
│   └── my-first-video/           # Blank project template — your starting point
├── docs/                         # Workflow guides
├── templates/                    # Project template + prompt cards
├── tools/                        # Setup & save scripts
└── final-outputs/                # Drop your best exports here
```

## Who this is for

Anyone building short AI video with Seedance 2.0, Kling, Runway, Veo, or similar. Especially useful if you're shipping ads, brand films, promoter reels, or lifestyle content and want a repeatable system instead of one-shot prompt roulette.

## Why this exists

If you've ever tried to one-shot a 30-second ad from a single prompt, you know the problem. The character drifts. The lighting jumps. The product mutates. You burn through credits chasing a "lucky render" that never lands.

The fix isn't a better prompt. It's working like a director instead of a slot machine — splitting the video into short, controllable shots, locking the moments that matter (faces, products, palette), and letting the AI fill the gaps between anchors you actually approved.

This repo is the system. You write a short brief, drop in your references, plan the shots, generate anchor frames you control, then animate between them and stitch the result. The folders walk you through each step and quietly stop you from skipping ahead before the last decision was locked.

It's not faster than slot-machine prompting on the first try. It's faster on the tenth — and the tenth one actually looks good.

## Quick start

### 1. Install the skill

```bash
cp -R skill/video-prompt-builder ~/.claude/skills/
```

Now Claude Code will trigger the skill whenever you describe a video brief.

### 2. Run setup

```bash
tools/setup-environment.sh --open
```

### 3. Open the demo first

```
projects/demo-avcc-workshop/
```

Watch `09-final-output/avcc-workshop-final-30s.mp4`, then walk backwards through the folders to see how it was built.

### 4. Create your own

Use the blank project at `projects/my-first-video/` or run:

```bash
tools/create-project.sh my-second-video
```

## The skill — `video-prompt-builder`

A Claude Code skill that turns a creative brief into a structured Seedance 2.0 prompt. It enforces six hard rules learned the hard way:

1. **Generation strategy gate** — always asks: one long multi-shot gen, or several stitched gens?
2. **Real people require real photos** — won't hallucinate a portrait of a specific person.
3. **VO word-distribution** — balances speech speed across stitched gens.
4. **Cost preflight** — declares Higgsfield Ultra credit cost before locking shot count.
5. **Image model routing** — GPT Image 2 for characters, Nano Banana Pro for off-state lighting, never silently swaps.
6. **Default architecture** — real-photo ref + structured shot list + b-roll cutaways + VO-synced timing.

Output is the four-section breakdown: shot timeline, effects inventory, density map, energy arc.

Full skill spec: [skill/video-prompt-builder/SKILL.md](skill/video-prompt-builder/SKILL.md)

## The folder rule

Every step has three subfolders:

```
attempts/      drafts go here
approved/      locked files go here
disapproved/   rejected files go here
```

Only build the next step from files in `approved/`. That's how you stop the project from becoming chaos.

## Workflow at a glance

```
01-creative-brief    →  what is this video about?
02-references        →  what must stay consistent?
03-shot-list         →  how does it break into shots?
04-image-prompts     →  prompts for first/last frames
05-storyboard-frames →  generated frame images
06-video-prompts     →  prompts to animate between frames
07-transition-videos →  generated clips
08-stitching         →  assemble and review seams
09-final-output      →  the export
```

## Tools

This stack is tool-agnostic. The default tested combo:

- **Image generation**: GPT Image 2 (high, 2k) for characters, Nano Banana Pro for off-state lighting
- **Video generation**: Seedance 2.0 via Higgsfield Ultra
- **Voiceover**: ElevenLabs
- **Stitching**: `ffmpeg`

But the process matters more than the tools. Swap any of them and the workflow still works.

## Demo: AVCC workshop reel

`projects/demo-avcc-workshop/` is a real 30-second 9:16 ad for the AVCC online workshop, built with two stitched 15-second multi-shot Seedance gens. Open `projects/demo-avcc-workshop/README.md` for a walkthrough.

