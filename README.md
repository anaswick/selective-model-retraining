# Selective Model Retraining Under Concept Drift

This repository contains the datasets, experimental artifacts, notebooks, configurations, and results accompanying the research paper:

**Selective Model Retraining: Balancing Predictive Robustness and Operational Efficiency under Concept Drift**

## Overview

Machine learning models deployed in production environments are often affected by **concept drift**, where data distributions evolve over time and gradually degrade predictive performance.

While periodic retraining is commonly used to maintain model quality, it can be computationally expensive and may not always be necessary. This study investigates whether **selective retraining** can achieve comparable or better predictive performance while significantly reducing retraining costs.

The repository provides all materials required to reproduce the experiments presented in the paper.

---

## Research Objectives

This study aims to:

1. Compare selective retraining against static and continuous retraining strategies.
2. Evaluate different memory mechanisms for model adaptation:

   * Cumulative Memory
   * Sliding Window
   * Exponential Decay
3. Compare:

   * Performance-based retraining triggers
   * PSI-based retraining triggers
4. Analyze the trade-off between:

   * Predictive performance
   * Temporal robustness
   * Retraining cost

---

## Experimental Strategies

Five retraining strategies are evaluated:

| Strategy                    | Description                                                             |
| --------------------------- | ----------------------------------------------------------------------- |
| No Retraining               | Static model trained once and never updated                             |
| Continuous Retraining       | Retrained after every batch                                             |
| Selective Cumulative        | Retrained only when triggered using all historical data                 |
| Selective Sliding Window    | Retrained only when triggered using recent observations                 |
| Selective Exponential Decay | Retrained only when triggered using exponentially weighted observations |

---

## Datasets

### Real-World Dataset

**Electricity Dataset**

* Source: OpenML Dataset ID 151
* Instances: 45,312
* Task: Binary Classification
* Target: Electricity price movement (UP / DOWN)

Dataset URL:

[https://www.openml.org/d/151](https://www.openml.org/search?type=data&sort=runs&id=151&status=active)

### Synthetic Datasets

Two synthetic datasets were generated from the Electricity dataset:

1. **Gradual Drift Dataset**

   * Progressive covariate and concept drift
   * Simulates slowly evolving environments

2. **Abrupt Drift Dataset**

   * Step-function distribution changes
   * Simulates sudden environmental shifts

---

## Repository Structure

```text
## Repository Structure

```text
.
├── data/
│   ├── raw/
│   │   └── electricity_dataset_info.md
│   │
│   └── synthetic/
│       ├── synthetic_gradual_drift.csv
│       └── synthetic_abrupt_drift.csv
│
├── notebooks/
│   ├── 1_electricity_data_preparation.ipynb
│   ├── 2_synthetic_dataset_generation.ipynb
│   ├── 3_drift_validation.ipynb
│   └── 4_simulation_retraining.ipynb
│   └── 5_analysis_and_result.ipynb
│
├── configs/
│   └── best_params.json
│
├── results/
│   ├── figures/
│   │   ├── objective_1/
│   │   │   ├── figure_O1_1_electricity_abrupt_concept_logreg.png
│   │   │   ├── figure_O1_1_electricity_abrupt_concept_xgb.png
│   │   │   └── ...
│   │   │
│   │   ├── objective_2/
│   │   │   ├── figure_O2_1_electricity_abrupt_concept_logreg_performance_trigger
│   │   │   ├── figure_O2_1_electricity_abrupt_concept_logreg_psi_trigger
│   │   │   └── ...
│   │   │
│   │   └── objective_3/
│   │       ├── figure_O3_1_combined_overall.png
│   │       ├── figure_O3_1_electricity.png
│   │       └── ...
│   │
│   └── tables/
│       ├── table_O1_1_electricity_abrupt_concept_logreg.csv
│       ├── table_O1_1_electricity_abrupt_concept_xgb.csv
│       └── ....csv
│
├── docs/
│   ├── data_availability_statement.md
│   └── author_contributions.md
│
├── requirements.txt
├── LICENSE
└── README.md
```

```

---

## Models

The following classifiers are evaluated:

* Logistic Regression (LR)
* XGBoost (XGB)

Hyperparameters were optimized using cross-validation on the initial training window.

The best configurations are provided in:

```text
configs/best_params.json
```

---

## Evaluation Metrics

### Predictive Performance

* Accuracy
* Mean Accuracy
* Standard Deviation of Accuracy

### Temporal Robustness

* Recovery Time
* Recovery Gain

### Retraining Cost

* Number of Retraining Events
* Total Retraining Data Volume

---

## Key Findings

### Selective Retraining Outperforms Static Models

Selective retraining consistently improves predictive performance over static models under concept drift.

### Continuous Retraining Is Not Always Optimal

Retraining after every batch results in substantially higher operational costs while often providing no additional accuracy benefits.

### Adaptive Forgetting Performs Best

Sliding Window and Exponential Decay memory mechanisms achieve the best balance between accuracy and retraining cost.

### Performance-Based Triggering Is More Cost-Efficient

Performance-driven retraining achieves comparable predictive accuracy while requiring substantially fewer retraining events and less retraining data than PSI-based triggering.

---

## Reproducing the Experiments

### 1. Clone Repository

```bash
git clone https://github.com/anaswick/selective-model-retraining.git
cd selective-model-retraining
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Run Notebooks

Execute notebooks sequentially:

```text
1_electricity_data_preparation.ipynb
2_synthetic_dataset_generation.ipynb
3_drift_validation.ipynb
4_simulation_retraining.ipynb
5_analysis_and_result.ipynb
```

Generated outputs will be stored in:

```text
results/
```

---

## Data Availability Statement

The datasets, experimental configurations, source code, and generated results supporting this study are publicly available in this repository.

The original Electricity dataset is publicly available through OpenML:

https://www.openml.org/d/151

Synthetic datasets generated for this study are included in the repository.

---

## Author Contributions (CRediT)

### Anas Wicaksono

* Conceptualization
* Methodology
* Software
* Formal Analysis
* Data Curation
* Visualization
* Writing – Original Draft

### Gede Putra Kusuma

* Supervision
* Methodology
* Validation
* Writing – Review & Editing

---

## Citation

If you use this repository, please cite the associated publication.

```bibtex
@article{wicaksono2026selective,
  title={Selective Model Retraining: Balancing Predictive Robustness and Operational Efficiency under Concept Drift under Concept Drift},
  author={Wicaksono, Anas and Kusuma, Gede Putra},
  year={2026}
}
```

---

## License

This repository is released for academic and research purposes.

Please refer to the LICENSE file for details.
