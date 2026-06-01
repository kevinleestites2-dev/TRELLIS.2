# TRELLIS.2 — Nexus Deployment Guide
**Forked for the Pantheon | Deployment Target: The Nexus (1TB Laptop)**

## Hardware Requirements
- GPU: 24GB VRAM minimum (RTX 3090 / 4090 / A100 / H100)
- RAM: 32GB+ recommended
- Storage: ~20GB for model weights + working space
- OS: Linux (required — not Windows, not Mac)
- CUDA: 12.4 recommended

## Pantheon Role
- **PropPilot:** Single listing photo → full 3D property render for buyer decks
- **ContentPrime:** Product image → rotating 3D asset for TikTok/YouTube content
- **Ghost Streamer:** 3D environment/prop generation for ghost persona backgrounds

## Quick Deploy (when Nexus is live)
```bash
git clone https://github.com/kevinleestites2-dev/TRELLIS.2
cd TRELLIS.2
. ./setup.sh --new-env --basic --flash-attn --nvdiffrast --nvdiffrec --cumesh --o-voxel --flexgemm
```

## Model Weights
- Auto-downloads from HuggingFace on first run: `microsoft/TRELLIS.2-4B`
- 4 Billion parameters | 512³ → 1536³ resolution output
- Full PBR materials: Base Color, Roughness, Metallic, Opacity

## Minimal Usage
```python
from trellis2.pipelines import Trellis2ImageTo3DPipeline
pipeline = Trellis2ImageTo3DPipeline.from_pretrained("microsoft/TRELLIS.2-4B")
pipeline.cuda()
from PIL import Image
image = Image.open("input.jpg")
outputs = pipeline.run(image)
# outputs contains mesh, texture, PBR maps
```

## Gradio Demo (local)
```bash
python app.py
# Opens at http://localhost:7860
```

## Notes
- Do NOT attempt on Red Magic — 24GB VRAM hard requirement
- Cloud option: RunPod A100 (~$1.50/hr) for testing before Nexus arrives
- Training code is included — fine-tuning on Florida property photos is possible
- Status: QUEUED — activate when Nexus is online
