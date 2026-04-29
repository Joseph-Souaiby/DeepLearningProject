# RoBERTa Full Fine-Tuning & LoRA — Experiment Results

---

## 1. Dataset Overview

| Dataset | Total (after dedup) | Human | AI | Train | Val | Test |
|---|---|---|---|---|---|---|
| **Kaggle** | 27,278 | 16,098 (59%) | 11,180 (41%) | 19,094 | 2,728 | 5,456 |
| **RAID** | 704,460 (full); 100,000 sampled | ~14% | ~86% | 69,999 | 10,000 | 20,000 |
| **RAID OOD eval** | 10,000 (balanced subset) | 5,900 | 4,100 | — | — | — (eval only) |

---

## 2. Model Configurations

| Model | Trainable Params | Total Params | Trainable % | LoRA rank / alpha |
|---|---|---|---|---|
| RoBERTa Full FT | 124,645,632 | 124,645,632 | 100% | — |
| RoBERTa LoRA r=8, α=16 | 294,912 | 124,940,544 | 0.2360% | r=8, α=16 |
| RoBERTa LoRA r=4, α=8 | 147,456 | 124,793,088 | 0.1182% | r=4, α=8 |
| RoBERTa LoRA r=2, α=4 | 73,728 | 124,719,360 | 0.0591% | r=2, α=4 |
| RoBERTa Frozen (head only) | ~1,538 | ~124.6M | ~0.001% | — |

---

## 3. Main Results

### 3.1 Trained on Kaggle

| Model | Kaggle Acc (%) | Kaggle F1 (macro) | RAID OOD Acc (%) | RAID OOD F1 (macro) | RAID Eval Loss |
|---|---|---|---|---|---|
| RoBERTa Full FT | **99.95** | **1.00** | 42.79 | 0.37 | 7.96 |
| RoBERTa LoRA r=8, α=16 | 99.16 | 0.99 | 40.97 | 0.32 | 4.85 |

### 3.2 Trained on RAID

| Model | RAID Acc (%) | RAID F1 (macro) | Kaggle OOD Acc (%) | Kaggle OOD F1 (macro) | RAID Eval Loss |
|---|---|---|---|---|---|
| RoBERTa Full FT | **94.06** | **0.93** | 50.22 | 0.45 | 0.307 |
| RoBERTa LoRA r=8, α=16 | 93.62 | 0.92 | 56.89 | 0.54 | 0.209 |
| RoBERTa LoRA r=4, α=8 | 93.94 | 0.92 | 59.90 | 0.58 | 0.162 |
| RoBERTa LoRA r=2, α=4 | 89.81 | 0.86 | 51.98 | 0.47 | 0.311 |
| RoBERTa Frozen | 81.47 | 0.72 | 41.29 | 0.30 | 0.390 |

---

## 4. Per-Class Breakdown (RAID-trained models, Kaggle OOD)

| Model | Human Prec | Human Recall | Human F1 | AI Prec | AI Recall | AI F1 |
|---|---|---|---|---|---|---|
| Full FT → Kaggle OOD | 1.00 | 0.16 | 0.27 | 0.45 | 1.00 | 0.62 |
| LoRA r=8 → Kaggle OOD | 0.99 | 0.27 | 0.43 | 0.49 | 0.99 | 0.65 |
| LoRA r=4 → Kaggle OOD | 1.00 | 0.32 | 0.49 | 0.51 | 1.00 | 0.67 |
| LoRA r=2 → Kaggle OOD | 1.00 | 0.19 | 0.31 | 0.46 | 1.00 | 0.63 |
| Frozen → Kaggle OOD | 1.00 | 0.01 | 0.01 | 0.41 | 1.00 | 0.58 |

---

## 5. LoRA Rank Ablation (RAID-trained, both eval sets)

| LoRA Rank | α | Trainable % | RAID Acc (%) | Kaggle OOD Acc (%) | RAID Loss |
|---|---|---|---|---|---|
| Full FT | — | 100% | 94.06 | 50.22 | 0.307 |
| r=8 | 16 | 0.236% | 93.62 | 56.89 | 0.209 |
| **r=4** | **8** | **0.118%** | **93.94** | **59.90** | **0.162** |
| r=2 | 4 | 0.059% | 89.81 | 51.98 | 0.311 |
| Frozen | — | ~0% | 81.47 | 41.29 | 0.390 |

---

## 6. Cross-Dataset Summary (All Models)

| Model | Train Set | In-Domain Acc (%) | OOD Acc (%) | OOD Δ vs. In-Domain |
|---|---|---|---|---|
| TF-IDF + LogReg **Baseline** | Kaggle | 99.12 | 40.86 | −58.3 pp |
| TF-IDF + LinearSVC **Baseline** | Kaggle | 99.74 | 40.90 | −58.8 pp |
| GLTR + LogReg **Baseline** | Kaggle | 95.42 | 57.78 | −37.6 pp |
| GLTR + LinearSVC **Baseline** | Kaggle | 95.64 | 55.20 | −40.4 pp |
| RoBERTa Full FT | Kaggle | 99.95 | 42.79 | −57.2 pp |
| RoBERTa LoRA r=8 | Kaggle | 99.16 | 40.97 | −58.2 pp |
| RoBERTa Full FT | RAID | 94.06 | 50.22 | −43.8 pp |
| RoBERTa LoRA r=8 | RAID | 93.62 | 56.89 | −36.7 pp |
| **RoBERTa LoRA r=4** | **RAID** | **93.94** | **59.90** | **−34.0 pp** |
| RoBERTa LoRA r=2 | RAID | 89.81 | 51.98 | −37.8 pp |
| RoBERTa Frozen | RAID | 81.47 | 41.29 | −40.2 pp |

---


