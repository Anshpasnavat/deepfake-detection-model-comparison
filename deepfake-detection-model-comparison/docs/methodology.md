# Experimental methodology and reporting notes

## Shared experiment framing

The notebooks describe experiments on a balanced 1,000-video selection from LAV-DF: 500 real and 500 fake clips, allocated to 600 training, 200 validation, and 200 test samples (300/300, 100/100, and 100/100 by class). A seed of 42 is used in the recorded configuration. The notebooks should be treated as the source of truth for exact preprocessing and split reuse.

## Saved thresholded test metrics

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC | TN | FP | FN | TP |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| AVoiD-DF | 0.6150 | 0.6292 | 0.5600 | 0.5926 | 0.6815 | 67 | 33 | 44 | 56 |
| AuViRe-inspired | 0.7200 | 0.7619 | 0.6400 | 0.6957 | 0.8018 | 80 | 20 | 36 | 64 |
| CCMA / MMMS-BA | 0.8000 | 0.7941 | 0.8100 | 0.8020 | 0.8323 | 79 | 21 | 19 | 81 |
| AVH-Align (Youden J operating point) | 0.7400 | 0.6846 | 0.8900 | 0.7739 | 0.7991 | 59 | 41 | 11 | 89 |

These values are taken from the saved notebook evaluation outputs and conference paper. AVH-Align's main comparison row uses the Youden J threshold. Its EER and max-F1 operating points are also available in the AVH-Align notebook.

## Separate AV-HuBERT linear-probe experiment

The AVH-Align notebook additionally fits a supervised logistic-regression linear probe on AV-HuBERT features. The saved probe output reports test AP `0.9884` and ROC-AUC `0.9866`. These are results of the separate feature-probe experiment, not the AVH-Align model's test metrics, and must not be mixed into the four-model comparison table.

## Model-specific deviations

- **AuViRe:** the supplied notebook explicitly labels the implementation as AuViRe-inspired and without the AV-HuBERT backbone; not a reproduction of the published full-dataset result.
- **CCMA / MMMS-BA:** notebook states it is adapted to two available modalities (visual and audio), rather than the original three-modality setup; it also documents a classification-only loss rather than the paper's full composite localization loss.
- **AVH-Align:** distinguish its AVH-Align training/evaluation workflow from the additional supervised linear-probe experiment.
- **AVoiD-DF:** report the implementation and subset protocol as documented in its notebook; do not imply full benchmark reproduction.

## Fair-comparison caution

Even where the split sizes and seed match, confirm identical sample IDs and preprocessing before making a strict head-to-head claim. Use the saved split metadata as evidence. Also distinguish threshold-dependent metrics (accuracy, precision, recall, F1) from threshold-free ranking metrics (ROC-AUC, AP).
