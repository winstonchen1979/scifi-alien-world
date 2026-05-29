# 🌌 Alien World Explorer

A sci-fi short video generated with **LTX-2.3** (22B) using sd.cpp.

## Scene Description

A lone astronaut in a sleek white spacesuit walks across the surface of an alien planet at twilight. Towering crystalline structures rise from the ground, glowing with bioluminescent purple and blue light. Two moons hang in a deep violet sky filled with colorful nebula clouds. The camera slowly follows the astronaut from behind as they approach a massive black alien monolith standing in the distance.

## Files

| File | Resolution | Size | Pipeline |
|------|------------|------|----------|
| `scifi_alien_world.webm` | 640x360 | 818KB | Single-stage |
| `scifi_alien_world_hq.webm` | **1280x768** | **2.0MB** | **Two-stage + Spatial Upscaler x2** |

## Technical Details (HQ Version)

| Parameter | Value |
|-----------|-------|
| Model | LTX-2.3 22B Dev (Q8_0 GGUF) |
| Text Encoder | Gemma-3 12B (Q8_0) |
| Base Resolution | 640x360 |
| Final Resolution | **1280x768** (x2 spatial upscale) |
| Frames | 33 (1.4s @ 24fps) |
| CFG Scale | 6.0 |
| Sampling | Euler, 20 steps + 4 hires refine |
| Upscaler | ltx-2.3-spatial-upscaler-x2-1.1 |
| GPU | AMD MI50 32GB (Device 1) |
| Runtime | ~12 minutes |

## Generation Command

```bash
HIP_VISIBLE_DEVICES=1 ./sd-cli \
  -M vid_gen \
  --diffusion-model ltx-2.3-22b-dev-Q8_0.gguf \
  --vae ltx-2.3-22b-distilled_video_vae.safetensors \
  --audio-vae ltx-2.3-22b-distilled_audio_vae.safetensors \
  --llm gemma-3-12b-it-Q8_0.gguf \
  --embeddings-connectors ltx-2.3-22b-distilled_embeddings_connectors.safetensors \
  --hires-upscalers-dir models/upscale_models \
  --hires-upscaler ltx-2.3-spatial-upscaler-x2-1.1 \
  --hires --hires-steps 4 \
  -p "A lone astronaut in a sleek white spacesuit walks across the surface of an alien planet at twilight..." \
  -n "worst quality, low quality, blurry, distorted, artifacts" \
  --cfg-scale 6.0 --sampling-method euler \
  -W 640 -H 360 --diffusion-fa --offload-to-cpu \
  --video-frames 33 --fps 24 \
  -o scifi_alien_world_hq.webm
```

## Tools Used

- [stable-diffusion.cpp](https://github.com/leejet/stable-diffusion.cpp) — C++ inference engine
- [LTX-2.3](https://github.com/Lightricks/LTX-2) — Video generation model by Lightricks
