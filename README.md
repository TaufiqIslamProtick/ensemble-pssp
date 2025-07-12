# Protein Secondary Structure Prediction using Deep Learning

This project investigates protein secondary structure prediction (PSSP) using deep learning. It evaluates existing predictors via ensemble voting and implements a custom neural network trained on PSSM profiles.

## Introduction

Protein structure is hierarchical—primary, secondary, tertiary, and quaternary. The secondary structure connects sequence to function. Experimental methods (e.g., X-ray crystallography, NMR) are accurate but expensive.

Three computational generations evolved:
- First-gen: Statistical models (e.g., Chou–Fasman)
- Second-gen: ML with sliding window (e.g., GOR)
- Third-gen: MSA + ML (e.g., SVMs, CRFs)

Recent approaches apply deep learning to capture complex, high-dimensional sequence patterns.

## Proposed Method

### Combined Voting Method

Four state-of-the-art PSSP server tools were used:

| Server         | Method                              | Q3 Accuracy |
|----------------|--------------------------------------|-------------|
| RaptorX        | Deep Convolutional Neural Fields     | 82.3%       |
| SPIDER2        | Iterative Deep Learning              | 81.9%       |
| Porter 4.0     | Bidirectional RNN                    | 82.0%       |
| Jpred4         | Ensemble of 2 ANNs                   | 77.1%       |

- **Unweighted Voting**: Equal weights → 82.76% accuracy  
- **Weighted Voting**: Based on Q3 scores → 87.48% accuracy  
- Ensemble voting outperformed all individual predictors

### Neural Network Implementation

Custom feed-forward neural network implemented in Java.

- Input: Sliding windows over PSSM (from DSSP dataset)
- Dataset: 50 proteins (45 training, 5 testing)
- Output: Three perceptrons (Helix, Sheet, Coil)
- Learning: Backpropagation

#### Key Experimental Results

- Best learning rate: 0.145–0.25
- Best window size: 13–19
- Best architecture: 3 hidden layers, ~150 perceptrons
- Sigmoid-scaling improved performance
- Maximum accuracy: 82.11%

## Results

### Combined Voting

| Predictor     | Accuracy (%) |
|---------------|--------------|
| RaptorX       | 82.67        |
| SPIDER2       | 82.07        |
| Porter 4.0    | 81.80        |
| JPred4        | 76.62        |
| Weighted Vote | **87.48**    |
| Unweighted    | 82.76        |

### Neural Network

| Parameter             | Best Accuracy (%) |
|-----------------------|-------------------|
| Learning Rate (0.25)  | 80.17             |
| Window Size (19)      | 81.07             |
| 350 Perceptrons (20 ep)| 82.11             |
| 3 Hidden Layers       | 81.96             |
| Sigmoided PSSM Input  | 80.65             |

## Discussion

- Ensemble methods improve robustness and accuracy over standalone predictors.
- Some predictors outperform others on specific proteins. A dynamic, protein-specific weighting system may enhance performance.
- The custom neural network is limited by feature diversity (only PSSM) and dataset size (50 proteins).
- Future work includes:
  - Automated PSSM generation (e.g., PSI-BLAST scripts)
  - Using larger datasets (e.g., CASP)
  - Exhaustive hyperparameter tuning

## Conclusion

- Weighted ensemble voting achieved 87.48% Q3 accuracy, surpassing all individual tools.
- The custom neural network showed promising performance with limited data and features.
- The framework can be improved via deeper feature integration, automated data pipelines, and larger datasets.

---

📄 See `PSSP_DL_Report.pdf` for full methodology, experiments, and analysis.
