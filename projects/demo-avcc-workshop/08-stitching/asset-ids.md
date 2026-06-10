# AVCC Workshop — Asset IDs (resume reference)

## Uploaded reference media (Higgsfield media_id)
- hero (Sergey studio): `7216c6d4-0059-4f58-81de-4b2e4076a179`
- b-roll drift (orig, has "BS" text): `cae1fc0f-b99d-4e35-83ea-a91aefaeea29`
- b-roll cockpit (orig, woman): `d8c2fa33-ab69-421a-bbd9-3af43a9b2812`
- b-roll fire (orig, has "creators" text): `139b8f88-a53b-4a9f-a309-a71eafcb4e1d`
- b-roll podium (orig, woman): `2105d994-7cf0-4d4c-9aa2-e58ecce02fde`

## Generated stills (nano_banana_pro, job_id → use as start_image for Seedance)
- cockpit-v1 (Sergey, frontal face): `3c8c5515-6cd2-486d-96ba-66053a822bc8`
- cockpit-v2 (Sergey, profile): `bc5a610a-cb9f-40db-906b-1a878a28a79a`
- podium-v1 (Sergey, smiling frontal): `8ead0ecd-319c-46bd-aa48-9eb5b71fe564`
- podium-v2 (Sergey, open track): `b74d154b-46bb-4129-8d3c-903f8ab7eee2`
- drift-clean (no text): `79a92080-a07c-48af-a8ab-1ed29d4a8ee3`
- fire-clean (no text): `5e4f4917-c13d-4579-a494-2cadc78dfa75`

Local copies in `05-storyboard-frames/`.

## Beat → start frame mapping (for the 8 Seedance gens)
- Beat 1 (Creator, 5s): hero media `7216c6d4...`
- Beat 2 (drift, 4s): drift-clean `79a92080...`
- Beat 3 (Driver, 4s): cockpit-v? (awaiting pick; default v1 `3c8c5515...`)
- Beat 4 (fire, 4s): fire-clean `5e4f4917...`
- Beat 5 (Creator, 4s): hero media `7216c6d4...`
- Beat 6 (Creator, 5s): hero media `7216c6d4...`
- Beat 7 (montage, 5s): cockpit-v2 `bc5a610a...` (driving angle)
- Beat 8 (Winner, 4s): podium-v? (awaiting pick; default v1 `8ead0ecd...`)

## Seedance settings
- model seedance_2_0, 720p, std, 9:16, duration 4–5s per beat. Cost 4s=18cr, 5s=22.5cr. Wave of 8 ≈ 158cr.
- VO baked into each prompt (see 06-video-prompts/seedance-prompts-v1.md). Voice-consistency across gens = watch item.

## FINAL APPROACH (chosen by Sergey): 2 × 15s videos, 1080p
Prompts: `06-video-prompts/seedance-prompts-v2-two15s.md`. 135 cr each, 270 total.
- Video 1 (beats 1-4) job: `594bd3c8-5638-4a2c-83ad-5cb081b25218` — start=hero, end=fire-clean, refs=drift+cockpit-v1
- Video 2 (beats 5-8) job: `eb347623-699f-4a85-bc12-171661fefc70` — start=hero, end=podium-v1, refs=cockpit-v2+drift

STATUS: both video jobs submitted & pending (1080p/15s seedance_2_0). Next: poll, download to 07-transition-videos/, review, stitch to 09-final-output.
