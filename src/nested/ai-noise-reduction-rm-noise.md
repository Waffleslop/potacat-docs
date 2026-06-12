# AI Noise Reduction (RM Noise)

[RM Noise](https://ournetplace.com/rm-noise/) is a free third-party Windows app that removes HF noise (QRN, static crashes, heterodynes) using AI models trained on real ham-radio recordings. POTACAT doesn't embed it, but you can route your receive audio through it today — and everything downstream of POTACAT, **including ECHOCAT listeners on your phone or remote desktop**, hears the cleaned-up audio.

## What you need

1. **RM Noise** — download from [ournetplace.com/rm-noise](https://ournetplace.com/rm-noise/)
2. **A virtual audio cable** — e.g. [VB-CABLE](https://vb-audio.com/Cable/) (free). Flex users already have DAX, which works as the input side.

## Routing

```
Radio RX audio (USB CODEC / DAX RX) → RM Noise → VB-CABLE → POTACAT audio input
```

1. In **RM Noise**: set its *input* to your rig's audio device (e.g. `USB Audio CODEC` or `DAX Audio RX 1`) and its *output* to `CABLE Input (VB-Audio)`.
2. In **POTACAT**: wherever you pick an audio input (ECHOCAT audio bridge, the VFO pop-out's monitor), choose `CABLE Output (VB-Audio)` instead of the rig's device.
3. Pick a noise model in RM Noise and listen — phone listeners over ECHOCAT get the same cleaned audio for free.

## Important: keep digital decoding on RAW audio

AI noise reduction is for **your ears, not for decoders**. It destroys the signal structure FT8/FT4, SSTV, and CW decoding depend on.

- In **JTCAT**, keep the audio source on the rig's raw device (`DAX Audio RX 1`, `USB Audio CODEC`, or SmartSDR Direct) — **not** the VB-CABLE device.
- Same for SSTV decoding.

Voice listening cleaned, digital decoding raw — best of both.

## Notes

- RM Noise is Windows-only, and some of its processing runs on its developer's servers, so it needs an internet connection.
- Expect a small added audio latency (the AI processes in blocks). Fine for ragchews and POTA hunting; irrelevant for digital since decoders bypass it.
- Native noise reduction inside POTACAT (no extra apps) is on the wishlist — if this routing works well for you, say so in [Discord](https://potacat.com/discord); it helps prioritize.
