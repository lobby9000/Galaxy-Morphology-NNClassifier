# Galaxy morphology classification with neural networks

Binary classification of galaxy images into early types (ellipticals, T-type ≤ 0) and late types (spirals and irregulars, T-type > 0) with convolutional networks and transfer learning.

**[Notebook](notebooks/galaxy-morphology-cnn.ipynb)** · [Versión en español](README.es.md)

## Highlights

- **5,608 galaxy images** from a MaNGA sample, split 70/15/15 into 3,924 training, 842 validation and 842 test images.
- **Baseline CNN:** 81.0% test accuracy, held back by a recall of only 0.68 on late types.
- **Improved models:** a deeper CNN reached **86.3%** test accuracy, and InceptionV3 transfer learning reached 85.9% with balanced recall (0.86 on both classes).

## Data

Images and a metadata table (`galaxias.csv`: name, T-type, bars, tidal features and g − i colour) are kept on [Google Drive](https://drive.google.com/drive/folders/1KO-0zXPLNNWNANdyPr38_gdFL9sT0Ovb?usp=sharing) because of their size. Labels come from the T-type: ≤ 0 is early (0) and > 0 is late (1).

## Models

| Model | Architecture | Test accuracy | Recall (early / late) |
|---|---|---|---|
| Baseline CNN | 2 × Conv2D (32, 64) with max pooling, Dense 64, dropout 0.5 | 81.0% | 0.89 / 0.68 |
| Deeper CNN | 3 × Conv2D (32, 64, 128), Dense 128, dropout 0.5, Adam (lr = 1e-4), early stopping with best-weight restore | 86.3% | 0.92 / 0.77 |
| InceptionV3 | Frozen ImageNet base with a sigmoid head | 85.9% | 0.86 / 0.86 |

All models take 150 × 150 RGB inputs and use binary cross-entropy with early stopping on validation loss.

## Known limitations

- The InceptionV3 experiment defines an augmentation pipeline (rotations, shifts, zoom and flips) but trains on the non-augmented generator. Wiring it in is the obvious next step.
- There is no class weighting yet, and early types are the majority class (514 vs 328 in the test set).

## Repository structure

```
├── notebooks/galaxy-morphology-cnn.ipynb   Experiments with saved outputs (Spanish comments)
└── docs/presentation-es.pdf                Final presentation (Spanish)
```

## Reproduce

```bash
pip install -r requirements.txt
jupyter notebook notebooks/galaxy-morphology-cnn.ipynb   # originally run on Google Colab
```

## Stack

Python · TensorFlow / Keras · scikit-learn · pandas · NumPy · Matplotlib · seaborn

## Context

Final project for *Introducción a Redes Neuronales*, Instituto de Astronomía, UNAM, taught by Dr José Antonio De Diego Onsurbe.

## Licence

Code released under the [MIT licence](LICENSE).

---

Part of the portfolio of Luis Ángel Quiroz López · [lobby9000.github.io](https://lobby9000.github.io) · [LinkedIn](https://www.linkedin.com/in/llqq) · [GitHub](https://github.com/lobby9000)
