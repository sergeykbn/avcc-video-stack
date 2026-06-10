# AVCC Online Workshop — Storyboard v3

**Format:** 9:16 vertical · ~30s · 2 × 15s Seedance 2.0 gens (std/1080p), stitched
**Hero:** Sergey (real photo `7216c6d4…`) — recurs as **Creator → Driver → Winner**
**Concept:** *"The system is the race machine — Sergey drives it while everyone else burns out."* Studio talking-head beats alternate with yellow GT3 RS motorsport b-roll, each insert literalizing the line being spoken.
**Voice:** generated inside Seedance, continuous across both gens (hero photo anchors the voice). Full script baked into each prompt.
**Text:** NO on-screen captions in the AI gen (model garbles text; locked decision from v2). Sergey can add his neon-yellow captions in post.
**Music:** none in deliverable — VO + ambient + transition SFX only.

---

## VO split (word-balanced for equal speech speed)

- **GEN 1 = 37 words** (lines 1–4)
- **GEN 2 = 38 words** (lines 5–10)

---

## GEN 1 — "The shift" (15s, 4 shots)

### Shot 1 — CREATOR (hook) · ~4.9s · line 1
**VO:** "This ad was created in 15 minutes with my new AI agent pipeline."
**Visual:** Sergey at his RGB studio desk, hands on the glowing keyboard, locks eyes with camera, slight confident nod.
**Camera:** slow push-in to a tight chest-up.
**Effect:** RGB bloom flare off the keyboard, subtle chromatic aberration.
**SFX:** studio room tone, soft mechanical key-clicks, low synth pad swell.
**Start frame:** hero `7216c6d4…`

### Shot 2 — B-ROLL drift · ~3.2s · line 2
**VO:** "The real advantage isn't tools or prompts anymore."
**Visual:** yellow Porsche 911 GT3 RS drifting through a track corner, thick tire smoke off the rear.
**Camera:** fast whip-pan tracking the car, speed-ramp into the apex.
**Transition IN:** whip-pan match-cut from Shot 1 (motion blur wipe).
**Effect:** motion blur, heat-haze shimmer.
**SFX:** engine roar + tire screech, whoosh on the cut.
**Start frame:** drift-clean `79a92080…`

### Shot 3 — DRIVER · ~3.6s · line 3
**VO:** "Building repeatable systems turns content creation into cash flow."
**Visual:** Sergey in the cockpit — AVCC yellow/black race suit, hands gripping the wheel, focused; world streaks past the side window.
**Camera:** dash-mounted, slight Dutch tilt, speed-ramp as he shifts.
**Transition IN:** smash zoom into the cockpit.
**Effect:** window speed-blur, rack focus to his eyes.
**SFX:** muffled engine drone, gear-shift clunk, breathing.
**Start frame:** cockpit-v1 `3c8c5515…` (Sergey, face-locked)

### Shot 4 — B-ROLL fire · ~3.2s · line 4
**VO:** "While most people just create random AI slop."
**Visual:** extreme close-up of the GT3 RS front wheel engulfed in flame, brake disc glowing, smoke curling — the "everyone else burning out" beat.
**Camera:** low-angle crash-zoom onto the burning wheel.
**Transition IN:** hard flash-cut.
**Effect:** ember sparks, fire glow, heat distortion.
**SFX:** fire crackle + metallic groan, bass impact on the cut.
**End frame of Gen 1:** fire-clean `5e4f4917…`

---

## GEN 1 → GEN 2 stitch
Hard **impact flash** match-cut from the fire glow into the bright studio — energy carries over the seam, voice continuous.

---

## GEN 2 — "The offer" (15s, 4 shots)

### Shot 5 — CREATOR (proof) · ~3.5s · line 5
**VO:** "Last month, I made over $50,000 with AI videos."
**Visual:** Sergey back at the studio desk, leans back with a confident half-smile, gestures once to camera.
**Camera:** punch-in from medium to close.
**Effect:** RGB bloom, quick light-streak behind him.
**SFX:** studio tone, subtle riser, single UI "ding."
**Start frame:** hero `7216c6d4…`

### Shot 6 — B-ROLL launch · ~4.3s · lines 6–7
**VO:** "That's exactly why I built my Skool community. Inside, you'll learn:"
**Visual:** the GT3 RS launches hard down the straight, rear squat, asphalt blurring — the machine accelerating.
**Camera:** low chase-cam, fast dolly, speed-ramp to hyper-speed.
**Transition IN:** light-streak wipe from Shot 5.
**Effect:** radial motion blur, lens flare streak.
**SFX:** turbo spool + roaring acceleration, whoosh.
**Start frame:** drift-clean `79a92080…` (re-angle to rear-launch)

### Shot 7 — DRIVER (the work) · ~4.7s · lines 8–9
**VO:** "Not just tools and prompts. Systems. Agent workflows. Everything we use ourselves."
**Visual:** Sergey driving — quick inserts of hands working the wheel and paddle-shifts, eyes locked on the track ("the workflows we run").
**Camera:** mounted rig, rapid micro-cuts synced to "Systems. Agent workflows.", Dutch tilt.
**Transition IN:** speed-ramp match-cut on motion.
**Effect:** rack focus hands→eyes, speed-blur.
**SFX:** engine build, rhythmic shift clunks punctuating each word.
**Start frame:** cockpit-v2 `bc5a610a…` (driving profile)

### Shot 8 — WINNER (CTA close) · ~2.4s · line 10
**VO:** "Over 5,000 creators are already inside."
**Visual:** Sergey on the podium, race suit, lifting the trophy overhead against the sponsor wall, triumphant.
**Camera:** crane-up reveal, slow-mo on the trophy raise.
**Transition IN:** whip-up tilt from cockpit to podium.
**Effect:** confetti / lens flare burst, golden bloom.
**SFX:** crowd cheer swell + shutter clicks, final boom-hit, then clean tail for VO.
**End frame of Gen 2:** podium-v1 `8ead0ecd…`

---

## Asset reuse (all already in project)
| Need | Asset | media/job id |
|---|---|---|
| Creator (start, shots 1 & 5) | hero studio photo | `7216c6d4…` |
| Driver shot 3 | cockpit-v1 (Sergey) | `3c8c5515…` |
| Driver shot 7 | cockpit-v2 (Sergey) | `bc5a610a…` |
| Winner shot 8 | podium-v1 (Sergey) | `8ead0ecd…` |
| Drift b-roll (shots 2 & 6) | drift-clean (no text) | `79a92080…` |
| Fire b-roll (shot 4) | fire-clean (no text) | `5e4f4917…` |

No new stills needed unless Sergey wants fresh driver/podium angles.

## Build plan after greenlight
1. `video-prompt-builder` skill → two 15s Seedance 2.0 prompts (4 shots each, VO baked, `generate_audio=true`).
2. Gen 1: start=hero, end=fire-clean, refs=drift+cockpit-v1.
3. Gen 2: start=hero, end=podium-v1, refs=cockpit-v2+drift.
4. Poll → download to `07-transition-videos/` → review identity/voice → ffmpeg concat to `09-final-output/`.
5. Est. cost ~270 cr (135/gen, 1080p) — no new stills.
