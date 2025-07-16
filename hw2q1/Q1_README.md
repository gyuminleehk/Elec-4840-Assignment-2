
# Q1 – Retinal Image Analysis using CLIP

This project explores the use of **Contrastive Language-Image Pretraining (CLIP)** using the **FLAIR retinal fundus dataset** for diabetic retinopathy classification on retinal fundus images.

---

## Objective

- Use CLIP to compute image-text similarity and classify diabetic retinopathy (DR) stages
- Apply prompt engineering for zero-shot learning
- Fine-tune CLIP on labeled fundus data for performance improvement

---

## Dataset

- Dataset: **FLAIR Retinal Fundus Images**
- Task: Predict Diabetic Retinopathy (DR) severity
- https://www.adcis.net/en/third-party/messidor2/

## How to Run

1. **Set up environment** (Tested on Google Colab or local with PyTorch + CLIP installed)
2. **Download fine-tuned model** using:

```bash
!gdown --id 1l24_2IzwQdnaa034I0zcyDLs_zMujsbR
```

> (Note: Due to code errors in other `.py` files, direct download was used)

3. **Run evaluation** with:

```python
python main_clip.py --image_path data/sample_fundus.jpg
```

---

## Additional Metrics

- Specificity and Negative Predictive Value (NPV) were calculated manually using the confusion matrix results from the prediction block:

```python
Specificity = TN / (TN + FP)
NPV = TN / (TN + FN)
```

---

## Results (After Fine-tuning)

| Metric          | Score     |
|-----------------|-----------|
| Accuracy        | 74.81%    |
| Weighted F1     | 0.720     |
| AUROC           | 0.8932    |
| Recall (Mild DR)| 0.00      |
| Recall (Severe) | 1.00      |

---

## Learnings

- CLIP + prompt engineering works surprisingly well for few-shot classification
- Finetuning image encoder improves recall for major classes
- Careful metric analysis beyond accuracy is essential

---

## Author

Lee Gyumin – HKUST ELEC 4840
