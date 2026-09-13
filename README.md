# Principal Component Analysis (PCA) on Breast Cancer and CIFAR-10

University / portfolio project that applies **Principal Component Analysis** to two very different datasets:

1. **Breast Cancer** (scikit-learn) — tabular medical features  
2. **CIFAR-10** (Keras) — 32×32 color images flattened to pixel vectors  

The goal is to see how much variance a few principal components keep, visualize the reduced space, and (for CIFAR-10) compare a small neural network trained on raw pixels vs PCA-compressed features.

## What’s in the repo

| File | Description |
|------|-------------|
| `PCA.ipynb` | Full analysis notebook (preferred) |
| `PCA.py` | Colab export of the same workflow |
| `Report.pdf` | Written project report |
| `cases.xlsx` | Supporting spreadsheet / case notes |

## Approach

### Breast Cancer
- Load and standardize features with `StandardScaler`
- Fit PCA with **2–5** components
- Plot 2D / 3D projections and bar charts of explained variance (and information lost)

### CIFAR-10
- Load images, flatten to feature vectors, scale
- Fit PCA with a small number of components for visualization
- Train a simple **Keras dense network** on:
  - original (flattened) features
  - PCA features that keep about **90% / 80% / 70% / 60% / 50%** of variance
- Compare training time and accuracy as dimensionality drops

## Key takeaways

- On Breast Cancer, a handful of PCs already explain a large share of variance (about **85% with 5 components** in this run), so the reduced view is still informative.
- On CIFAR-10 pixel data, variance is spread across many dimensions; a few PCs are not enough for a faithful image representation.
- Training on PCA features can speed up epochs, but pushing variance retention too low hurts validation accuracy quickly.

Exact numbers depend on the run; open `PCA.ipynb` or `Report.pdf` for plots and tables from the completed experiment.

## Tech stack

Python, NumPy, Pandas, Matplotlib, Seaborn, scikit-learn, TensorFlow / Keras, Jupyter

## How to run

```bash
git clone https://github.com/mahmouduskudar/principal-component-analysis-pca-on-breast-cancer-and-cifar-10-datasets.git
cd principal-component-analysis-pca-on-breast-cancer-and-cifar-10-datasets
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install numpy pandas matplotlib seaborn scikit-learn tensorflow jupyter tabulate
jupyter notebook PCA.ipynb
```

CIFAR-10 downloads automatically through Keras the first time you run the notebook.
