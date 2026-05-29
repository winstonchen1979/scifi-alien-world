# 🌌 Alien World Explorer

A sci-fi short video generated with **LTX-2.3** (22B) using sd.cpp.

## Scene Description

A lone astronaut in a sleek white spacesuit walks across the surface of an alien planet at twilight. Towering crystalline structures rise from the ground, glowing with bioluminescent purple and blue light. Two moons hang in a deep violet sky filled with nebula clouds. The camera slowly follows the astronaut as they approach a massive alien monolith.

## Technical Details

| Parameter | Value |
|-----------|-------|
| Model | LTX-2.3 22B Dev (Q8_0 GGUF) |
| Text Encoder | Gemma-3 12B (Q8_0) |
| Resolution | 640x360 |
| Frames | 33 (1.4s @ 24fps) |
| CFG Scale | 6.0 |
| Sampling | Euler, 20 steps |
| GPU | AMD MI50 32GB (Device 1) |
| Runtime | ~6 minutes |

## Generation Command

```bash
HIP_VISIBLE_DEVICES=1 ./sd-cli \
  -M vid_gen \
  --diffusion-model ltx-2.3-22b-dev-Q8_0.gguf \
  --vae ltx-2.3-22b-distilled_video_vae.safetensors \
  --audio-vae ltx-2.3-22b-distilled_audio_vae.safetensors \
  --llm gemma-3-12b-it-Q8_0.gguf \
  --embeddings-connectors ltx-2.3-22b-distilled_embeddings_connectors.safetensors \
  -p "A lone astronaut in a sleek white spacesuit walks across the surface of an alien planet at twilight..." \
  --cfg-scale 6.0 --sampling-method euler \
  -W 640 -H 360 --diffusion-fa --offload-to-cpu \
  --video-frames 33 --fps 24 \
  -o scifi_alien_world.webm
```

## Tools Used

- [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp) — C++ inference engine
- [LTX-2.3](https://github.com/Lightricks/LTX-Video) — Video generation model by Lightricks
