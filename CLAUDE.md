# Claude Code Setup Instructions — AVCC Video Stack

When someone clones this repo and asks Claude Code to "set this up", follow this flow.

## 1. Install the skill

The `skill/video-prompt-builder/` directory bundles a Claude Code skill that enforces six hard rules for Seedance 2.0 prompts. Install it before starting any video work:

```bash
cp -R skill/video-prompt-builder ~/.claude/skills/
```

The skill triggers automatically on briefs that mention video prompts, Seedance, shot lists, ad concepts, brand films, or storyboards.

## 2. Run environment setup

```bash
tools/setup-environment.sh --open
```

This opens the project folders in Finder.

## 3. Show the user the two starting points

- `projects/demo-avcc-workshop/` — the finished clickable example (30-second AVCC workshop ad). Walk them through it to show the full workflow.
- `projects/my-first-video/` — the blank project they will use for their own video.

## 4. Start the user at the brief

Open `projects/my-first-video/01-creative-brief/` and ask:

> Do you want approval at every step, or should I use autopilot and only stop if something is risky or unclear?

## 5. Folder rules

Every step has three subfolders:

- `attempts/` — drafts and experiments
- `approved/` — locked decisions (only build the next step from these)
- `disapproved/` — rejected versions, kept for reference

## 6. When the user asks for video prompts

The `video-prompt-builder` skill takes over. It will:

1. Ask whether they want one long multi-shot Seedance gen or several stitched gens (Rule 1 gate)
2. Verify real-person photos are attached if the brief features a specific person (Rule 2)
3. Balance VO word distribution across gens if VO is present (Rule 3)
4. Declare estimated Higgsfield Ultra credit cost before locking shot count (Rule 4)
5. Route image generation to the right model (Rule 5)
6. Apply the default architecture (Rule 6)

Then produce the four-section output: shot timeline, effects inventory, density map, energy arc.

## 7. Save progress to GitHub (optional)

If the user wants to back up their work:

```bash
tools/save-to-github.sh "Save storyboard project progress"
```

Do not delete `projects/demo-avcc-workshop/`. It is the teaching walkthrough.
