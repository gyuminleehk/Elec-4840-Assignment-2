
# Q2 – Spleen CT Segmentation with 3D U-Net 

This project applies a 3D U-Net to segment **3D abdominal CT images containing spleen**, provided in `.nii.gz` format. spleen regions in abdominal CT scans, evaluate performance using Dice and HD, and visualize predictions.

---

## Dataset

- Format: `.nii.gz` 3D CT scans
- Preprocessed into patches of 96×96×32
- https://drive.google.com/file/d/1dxRiLfJKD_he9a6mLFl2mzGzdKvq2ocn/view

## Model Setup

- Input: `.nii.gz` 3D CT volumes with spleen masks
- Sliding window inference: 96×96×32 patches
- Loss: Dice + CrossEntropy hybrid loss (α = 0.5)
- Optimizer: Adam
- Early stopping: Patience = 45 epochs

---

## How to Run

1. **Prepare dataset**  
   Save dataset to:

```
/content/drive/MyDrive/elec4840/Code_Template_new/Q2/SpleenDataset
```

or modify the following in `train_unet.py`:

```python
data_dir = "/your/custom/dataset/path"
```

2. **Training**  
   Run all cells before the “Inference and Report Performance on Test Set” block.

3. **TensorBoard Visualization (Optional)**

In Google Colab:
```python
%load_ext tensorboard
%tensorboard --logdir runs
```

→ If running locally, TensorBoard logs might not persist.  
To address this, **Dice/Val and Loss/Train graphs** were saved in `.png` format and included in `/images`.

---

## Visualization

- Best prediction slices are visualized using `Test Image, Test mask, Prediction mask` block.
- Make sure to create the `predict/` folder under `SpleenDataset/`
- Predicted results are saved as `.nii.gz` and visualized using ITK-SNAP

🖼 If visualization fails:
- PNG overlays of each test prediction were saved manually in `images/` using ITK-SNAP

---

## Performance

| Metric         | Value (Excl. Outlier) |
|----------------|------------------------|
| Dice           | 0.8639                |
| ASD            | 4.01 mm               |
| 95HD           | 20.27 mm              |

`best_model.pth` was saved during training and used for final evaluation.

---

## Additional Notes

| Loss Type       | Dice Score | ASD (mm) |
|------------------|------------|-----------|
| CrossEntropy     | 0.0012     | 240.08    |
| Dice             | 0.0184     | 196.25    |
| Hybrid (α=0.5)   | **0.0585** | **152.92** |

---

## Author

Lee Gyumin – HKUST ELEC 4840
