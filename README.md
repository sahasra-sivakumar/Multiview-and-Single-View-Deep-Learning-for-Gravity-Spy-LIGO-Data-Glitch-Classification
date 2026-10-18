# Multiview Deep Learning for LIGO Glitch Classification

Comparing a four-view attention-based convolutional network with single-view transfer-learning baselines on Gravity Spy spectrograms.

Author: Sahasra Sivakumar  
Report date: July 2026

## Research question

Can combining aligned spectrograms of the same glitch at different time durations improve classification relative to single-view models?

## Approach

The project considers 22 glitch classes and four duration views: 0.5, 1.0, 2.0, and 4.0 seconds.

- Preprocessing organizes data by split, duration, and class while aligning views by event identifier.
- GSMultiViewNet uses four CNN branches with Inception–ResNet-inspired residual modules.
- A gated attention mechanism combines branch representations into a prediction.
- VGG19 and InceptionV3 provide pretrained single-view baselines.

The report uses 448 × 448 inputs for the multiview network, 224 × 224 for VGG19, and 299 × 299 for InceptionV3.

## Reported results

| Model | Test accuracy | Training epochs |
|---|---:|---:|
| GSMultiViewNet | 96.19% | 26, early stopping |
| VGG19 | 92.20% | 30 |
| InceptionV3 | 86.86% | 30 |

The reported accuracy differences are 3.99 percentage points versus VGG19 and 9.33 percentage points versus InceptionV3. These figures come from the project report and have not been independently reproduced for this README.

## Training and evaluation

The report describes cross-entropy training, Adam optimization, and validation-based checkpoint selection. The multiview model additionally uses label smoothing and separate weight-decay settings for feature extraction and fusion. Evaluation includes learning curves, confusion matrices, and classification reports.

## Repository contents

- [Main notebook](<Gravity-Spy NNDL Project.ipynb>)
- [Full project report](<GravitySpy NNDL_project_report.pdf>)

## Running the project

Open the notebook in a Jupyter-compatible Python environment. Before execution, inspect imports, dataset paths, preprocessing cells, and checkpoint locations. Obtain the appropriate Gravity Spy data and configure paths to match the notebook.

A verified dataset-download procedure, dependency lockfile, hardware specification, and clean-environment run instructions remain to be documented. The report alone does not establish that the repository runs without local changes.

## Interpretation and limitations

The comparison changes input information, image resolution, model architecture, learning rate, and training settings. It demonstrates the performance of these reported configurations, not an isolated causal effect of attention fusion. Additional controlled ablations are needed to separate these factors.

Before treating the results as a reproducible benchmark, verify event-level separation across train, validation, and test sets; consistent alignment and label mappings; the chosen single-view duration; class-wise metrics; and variation across random seeds. Lower loss alone is not sufficient evidence of better probability calibration.

## Project scope

This is a scientific image-classification project using Gravity Spy representations, not a deployed LIGO detection pipeline. The report is the source of the architecture and results summarized here.

## Related work cited in the report

- J. Glanzer et al., “Data quality up to the third observing run of Advanced LIGO: Gravity Spy glitch classifications,” Classical and Quantum Gravity 40, 065004 (2023).
- Y. Wu et al., “Advancing glitch classification in Gravity Spy: multi-view fusion with attention-based machine learning for Advanced LIGO’s fourth observing run,” Classical and Quantum Gravity 42, 165015 (2025).
