# LoRAx3DSeg

Unified repository for LoRA-based medical image segmentation experiments on 2D and 3D datasets.

## Contributors

Joseph Gavareshki Margaryan, Carlo Rosso, Gaetano Tedesco, Gabriel Sainz Vazquez

## Repository Structure

This repository integrates two independent projects:

- **3D/** - 3D medical segmentation ([medlora-3d](https://github.com/josephmargaryan/medlora-3d.git))
- **2D/** - 2D polyp segmentation ([SEG-PEFT](https://github.com/rossoc/SEG-PEFT.git))

## Quick Start

### 3D Segmentation

```bash
cd 3D
pip install monai nibabel
pip install -e . --no-deps

python main.py \
  --model swinv1 \
  --dataset Task03_Liver \
  --method lora \
  --train-fraction 20 \
  --epochs 50 \
  --batch-size 2 \
  --lora-r 8 \
  --lora-alpha 16
```

**Available datasets:** Task01_BrainTumour, Task02_Heart, Task03_Liver, Task04_Hippocampus, Task05_Prostate, Task06_Lung, Task07_Pancreas, Task08_HepaticVessel, Task09_Spleen, Task10_Colon

**Methods:** `lora` | `fft` (full fine-tuning)

### 2D Segmentation

Download [Kvasir-SEG dataset](https://datasets.simula.no/downloads/kvasir-seg.zip) and place in `2D/data/Kvasir-SEG/`

```bash
cd 2D
pip install -r requirements.txt

# Full fine-tuning
python scripts/train_segformer.py --epochs 30 --lr 5e-5 --save-dir experiment_fft

# LoRA
python scripts/train_segformer_lora.py --epochs 30 --lr 5e-5 --rank 8 --lora-alpha 32 --save-dir experiment_lora
```

## References

- 3D implementation: [josephmargaryan/medlora-3d](https://github.com/josephmargaryan/medlora-3d.git)
- 2D implementation: [rossoc/SEG-PEFT](https://github.com/rossoc/SEG-PEFT.git)