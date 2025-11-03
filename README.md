# Minimal NeRF Demo (LEGO)

This project adapts the core ideas from [yenchenlin/nerf-pytorch](https://github.com/yenchenlin/nerf-pytorch) into a compact training script that targets a **single** NeRF dataset: the synthetic LEGO scene from the original NeRF paper. The goal is to provide a straightforward, presentation-friendly demo without the extra configuration layers required for multiple datasets or advanced features.

## Setup

1. Install the Python dependencies:
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```

2. Download the synthetic LEGO dataset from the original repository and place it at `data/nerf_synthetic/lego`. The directory should contain images (`*.png`) and the `transforms_*.json` files.

## Training

Launch the training script:
```bash
python train_lego.py
```

The script trains a single NeRF network for the LEGO scene, writing checkpoints and a few rendered validation images to `outputs/`. Training defaults to a short schedule suitable for live demonstrations (20k iterations); tweak hyperparameters inside `train_lego.py` if you need longer runs or higher quality.

## Outputs

- `outputs/checkpoint_latest.pt`: latest model weights.
- `outputs/render_step_<iter>.png`: validation view rendered every 5k iters.
- `outputs/metrics.json`: quick log of loss and PSNR at render intervals.

## Notes

- Only the LEGO dataset is supported. Paths and camera parameters are hard-coded for the Blender-style JSON format.
- The implementation keeps just the essentials: a single NeRF (coarse) network, positional encoding, and stratified sampling along rays.
- For reproducibility, a fixed random seed is set inside the training script.
