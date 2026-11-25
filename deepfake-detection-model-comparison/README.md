# Deepfake Detection: Four-Model Comparison on LAV-DF

A research project comparing four audio-visual deepfake detection approaches using a balanced 1,000-video experiment on the **Localized Audio-Visual Deepfake (LAV-DF)** dataset.

> **Reproducibility note:** The reported values below are the saved outputs in the supplied notebooks. They are experiment-specific results on a selected 1,000-video subset, not claims that reproduce the original papers' full-dataset benchmarks. Read each notebook's model-specific notes before interpreting results.

## Models included

1. **AVoiD-DF** — an implementation of the AVoiD-DF architecture described in the notebook.
2. **AuViRe-inspired** — the supplied notebook explicitly labels this as an inspired/adapted implementation without the AV-HuBERT backbone; it is not a reproduction of the paper's published numbers.
3. **CCMA / MMMS-BA** — the supplied notebook describes an adaptation to the two modalities available in this pipeline (visual and audio), rather than the original three-modality setup.
4. **AVH-Align** — the notebook reports retrained AVH-Align test metrics at multiple operating points. The main comparison uses the **Youden J** operating point (the same values reported in the conference paper). The notebook also includes a separate AV-HuBERT-feature linear-probe experiment; its AP/AUC must not be attributed to AVH-Align.

## Repository structure

```text
deepfake-detection-model-comparison/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   ├── AuViRe_LAVDF_1000.ipynb
│   ├── AVH_Align_LAVDF_1000.ipynb
│   ├── AVoiD_DF_LAVDF_1000.ipynb
│   └── CCMA_MMMS_BA_LAVDF_1000.ipynb
├── dataset/
│   └── README.md
├── results/
│   └── comparison.csv
└── docs/
    └── methodology.md
```

## Experiment setup

The supervised notebook experiments describe a balanced subset with:

| Split | Total videos | Real | Fake |
|---|---:|---:|---:|
| Training | 600 | 300 | 300 |
| Validation | 200 | 100 | 100 |
| Testing | 200 | 100 | 100 |
| **Total** | **1,000** | **500** | **500** |

The notebooks use a fixed random seed of 42 in their experiment configuration. The saved AuViRe and CCMA reports also specify AdamW, learning rate `0.0001`, batch size `4`, and `5` epochs. Refer to each notebook for its exact model-specific preprocessing, training protocol, and deviations.

## Saved test results

The main comparison below uses the thresholded test results reported in the conference paper and the supplied notebooks. For AVH-Align, the paper uses the Youden J operating point.

| Experiment | Accuracy | Precision | Recall | F1-score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| AVoiD-DF | 61.50% | 62.92% | 56.00% | 59.26% | 0.6815 |
| AuViRe-inspired (adapted) | 72.00% | 76.19% | 64.00% | 69.57% | 0.8018 |
| CCMA / MMMS-BA (adapted) | 80.00% | 79.41% | 81.00% | 80.20% | 0.8323 |
| AVH-Align (Youden J operating point) | 74.00% | 68.46% | 89.00% | 77.39% | 0.7991 |

**Interpretation:** CCMA / MMMS-BA has the highest accuracy, F1-score, and ROC-AUC in this experiment. AVH-Align has the highest recall (89.00%) but also the most false positives (41). AuViRe-inspired has the fewest false positives (20). AVoiD-DF has the lowest score on all five reported metrics.

AVH-Align is threshold-dependent for accuracy, precision, recall, and F1. Its notebook also reports EER and max-F1 operating points; see the notebook for those alternatives. A separate AV-HuBERT-feature linear-probe experiment reports AP 0.9884 and ROC-AUC 0.9866. Those probe values are **not** the AVH-Align results in the table and must not be presented as such.

## Hardware and execution environment

The experiment notes refer to Kaggle GPU notebooks and NVIDIA Tesla T4 hardware. The AVH-Align notebook uses a staged workflow with external AV-HuBERT/upstream components. Exact GPU availability, CUDA, PyTorch, and dependency compatibility depend on the runtime session.

## How to run

1. Clone or download this repository.
2. Obtain access to the LAV-DF dataset and accept any dataset terms required by its maintainers.
3. Open the desired notebook in a compatible Kaggle environment.
4. Attach the LAV-DF dataset to the notebook and verify the dataset root/path discovery step.
5. Install or verify the notebook's dependencies.
6. Run the notebook cells in order.
7. Review the notebook's final evaluation and reproducibility notes.

The notebooks were originally authored around Kaggle paths such as `/kaggle/input/` and `/kaggle/working/`. They may require path changes and dependency adjustments in a local environment.

## Dataset

The dataset is **not included** in this repository. See [`dataset/README.md`](dataset/README.md) for access and setup notes.

## Important research limitations

- These experiments use a selected 1,000-video subset, not the complete LAV-DF benchmark.
- Model adaptations are not identical to the original papers' complete architectures or training protocols; each notebook documents its differences.
- AuViRe is explicitly an inspired/adapted implementation without the AV-HuBERT backbone.
- CCMA / MMMS-BA is adapted to audio and visual modalities; its notebook notes that the official paper uses a three-modality setup and additional localization supervision.
- AVH-Align's saved linear-probe metrics are for a separate AV-HuBERT-feature probe, not the AVH-Align model. Report them under the correct name.
- Results can vary with dataset version, runtime, preprocessing, random state, and dependency versions.

## Research paper context

The companion conference paper is titled **“Evaluation of Existing Audio-Visual Deepfake Detection Models on the LAV-DF Dataset”** and lists Ansh Pasnavat, Simran Sanya, Vansika Mishra, Sandeep Kumar, and Rohit Kumar Sachan (Sharda University). The paper is used as a source for the research framing, methodology, model descriptions, comparison metrics, and discussion; the PDF itself is intentionally not included in this repository.

## Citation and attribution

Please cite the original papers and dataset documentation when using the corresponding architectures or data. The conference-paper bibliography includes the original AVoiD-DF, AuViRe, CCMA/MMMS-BA, AVH-Align, and LAV-DF references. This repository does not claim ownership of the original model designs or dataset.

## License

No license is included yet. Add a license only after confirming that you have the right to redistribute your own code and that the chosen license is compatible with the upstream model code and dataset terms.
