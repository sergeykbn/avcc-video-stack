# AVCC Online Workshop — Seedance 2.0 prompt v5 (2 × 15s, lip-sync)

**Why:** single-15s gen over-compressed the full script. Reverting to the proven 2×15s architecture → 30s total at ~2.5 wps (comfortable). Stitched with ffmpeg.

**Jobs (720p / 15s / 9:16 / std / action):**
- Part 1 (lines 1–4): `0aec250c-2cd0-412a-ab70-d417e1350c65` — start=hero `7216c6d4…`, end=fire-clean `5e4f4917…`, refs=cockpit-v1 `3c8c5515…`, drift-clean `79a92080…`
- Part 2 (lines 5–10): `23f5adc4-75d8-4fc7-afaa-9b809da6a563` — start=hero `7216c6d4…`, end=podium-v1 `8ead0ecd…`, refs=cockpit-v2 `bc5a610a…`, drift-clean `79a92080…`

## Lip-sync approach
- Spoken lines land on **front-facing STUDIO shots** (mouth visible) → prompt forces precise lip-sync, mouth shapes per syllable.
- Motorsport / cockpit / podium shots = same voice as **voiceover** (no on-screen mouth to sync).
- Hero studio photo = start_image of BOTH gens → anchors one consistent voice across the stitch.

## VO map
**Part 1:** S1 studio(lipsync) "This ad was created in 15 minutes with my new AI agent pipeline." · S2 drift(VO) "The real advantage isn't tools or prompts anymore." · S3 studio(lipsync) "Building repeatable systems turns content creation into cash flow." · S4 fire(VO) "While most people just create random AI slop."
**Part 2:** S1 studio(lipsync) "Last month, I made over fifty thousand dollars with AI videos." · S2 launch(VO) "That's exactly why I built my Skool community. Inside, you'll learn:" · S3 cockpit(VO) "Not just tools and prompts. Systems. Agent workflows. Everything we use ourselves." · S4 podium(VO) "Over five thousand creators are already inside."

## Stitch
ffmpeg concat (same 720p/codec) → `09-final-output/avcc-online-workshop-v5-30s.mp4`. Seam: P1 ends on fire→white flash, P2 opens on studio bloom-flash → clean match.
