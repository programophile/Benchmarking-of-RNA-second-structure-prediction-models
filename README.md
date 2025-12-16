# Benchmarking of RNA Secondary Structure Prediction Models

A comprehensive benchmarking suite for evaluating and comparing various deep learning models for RNA secondary structure prediction. This repository implements and compares multiple neural network architectures including BiLSTM, CNN, Transformer, and trRosettaRNA models.

## Overview

RNA secondary structure prediction is a fundamental problem in computational biology. This project provides a unified framework to benchmark different deep learning approaches for predicting RNA secondary structures from nucleotide sequences. The models predict base-pairing patterns using dot-bracket notation.

## Features

- **Multiple Model Architectures**: Implementation of 4 different deep learning models
  - BiLSTM (Bidirectional Long Short-Term Memory)
  - CNN (Convolutional Neural Network)
  - Transformer (Self-Attention based)
  - trRosettaRNA (State-of-the-art wrapper)

- **Comprehensive Benchmarking**: Side-by-side comparison with standardized evaluation metrics
  - Precision, Recall, F1-Score
  - Accuracy
  - Training time and parameters

- **Ablation Studies**: 
  - BiLSTM variations (different architectures and configurations)
  - Transformer variations (position encoding, attention heads, dropout)

- **Production-Ready Code**: Clean, modular implementations with proper data handling

## Dataset

The project uses the **bpRNA-new** dataset from the [multimolecule](https://huggingface.co/datasets/multimolecule/bprna-new) Hugging Face repository:
- **Size**: 5,401 RNA sequences
- **Splits**: Train (3,200), Validation (800), Test (1,000)
- **Format**: Parquet files with sequences and secondary structures in dot-bracket notation
- **Structure**: Each sample contains an RNA sequence (A, C, G, U nucleotides) and corresponding secondary structure

## Installation

### Prerequisites

- Python 3.7+
- CUDA-capable GPU (recommended for training)
- Git

### Setup

1. Clone this repository:
```bash
git clone https://github.com/programophile/Benchmarking-of-RNA-second-structure-prediction-models.git
cd Benchmarking-of-RNA-second-structure-prediction-models
```

2. Install required dependencies:
```bash
pip install torch torchvision torchaudio
pip install pandas numpy scikit-learn matplotlib
pip install datasets huggingface-hub
pip install jupyter notebook
```

3. The trRosettaRNA2 repository will be automatically cloned when running the main benchmark notebook.

## Usage

### Running the Full Benchmark

Open and run the main benchmark notebook:

```bash
jupyter notebook code.ipynb
```

This notebook will:
1. Load and preprocess the bpRNA-new dataset
2. Train all models (BiLSTM, CNN, Transformer, trRosettaRNA)
3. Evaluate each model on the test set
4. Display comparative results with visualizations

### Running Ablation Studies

**BiLSTM Ablation Study:**
```bash
jupyter notebook bilstm.ipynb
```

Explores variations of BiLSTM architecture including:
- Different hidden layer sizes
- Various numbers of LSTM layers
- Bidirectional vs. unidirectional configurations

**Transformer Ablation Study:**
```bash
jupyter notebook transformer-abalation.ipynb
```

Evaluates transformer variants:
- With/without positional encoding
- Different numbers of attention heads
- Impact of dropout

## Models

### 1. BiLSTM (Bidirectional LSTM)
- **Architecture**: Embedding → BiLSTM → Dropout → Linear
- **Parameters**: ~199K
- **Strengths**: Captures sequential dependencies in both directions

### 2. CNN (Convolutional Neural Network)
- **Architecture**: Embedding → Conv1D → ReLU → MaxPool → Linear
- **Strengths**: Fast training, good at capturing local patterns

### 3. Transformer
- **Architecture**: Embedding → Positional Encoding → Transformer Encoder → Linear
- **Parameters**: Configurable (64-dim embeddings, 4 heads, 3 layers by default)
- **Strengths**: Self-attention mechanism, parallel processing

### 4. trRosettaRNA Wrapper
- **Type**: Pre-trained state-of-the-art model
- **Source**: [trRosettaRNA2 repository](https://github.com/quailwwk/trRosettaRNA2)
- **Strengths**: Based on proven architecture from protein structure prediction

## Notebooks

### `code.ipynb` - Main Benchmarking Suite
The primary notebook containing:
- Complete data loading and preprocessing pipeline
- All model implementations
- Training and evaluation loops
- Comparative analysis and visualization
- Performance metrics for all models

### `bilstm.ipynb` - BiLSTM Ablation Study
Focused analysis of BiLSTM variations:
- Architecture component analysis
- Hyperparameter sensitivity studies
- Performance vs. complexity trade-offs

### `transformer-abalation.ipynb` - Transformer Ablation Study
Systematic evaluation of transformer components:
- Positional encoding impact
- Attention head configurations
- Regularization effects (dropout)

## Evaluation Metrics

All models are evaluated using:
- **Precision**: Ratio of correctly predicted base pairs to total predicted pairs
- **Recall**: Ratio of correctly predicted base pairs to actual base pairs
- **F1-Score**: Harmonic mean of precision and recall
- **Accuracy**: Overall correctness of predictions
- **Training Time**: Time required to train the model
- **Model Parameters**: Total number of trainable parameters

## Results

The benchmark compares all models on the same test set, providing:
- Performance metrics table
- Training curves (loss and validation F1)
- Confusion matrices
- Computational efficiency analysis

*(Run the notebooks to see actual results)*

## Data Format

**Input**: RNA sequences as strings
```
ACUGGUUGCGGCCAGUAUAAAUAGUCUUUAAGCCGCAAGCGUGUCC...
```

**Output**: Secondary structure in dot-bracket notation
```
((((........)))).........((..............(((((...
```

Where:
- `(` indicates the 5' end of a base pair
- `)` indicates the 3' end of a base pair
- `.` indicates an unpaired base

## Requirements

Core dependencies:
- `torch` >= 1.9.0
- `numpy` >= 1.19.0
- `pandas` >= 1.3.0
- `scikit-learn` >= 0.24.0
- `matplotlib` >= 3.3.0
- `datasets` (Hugging Face)
- `jupyter`

## Project Structure

```
.
├── code.ipynb                      # Main benchmarking notebook
├── bilstm.ipynb                    # BiLSTM ablation study
├── transformer-abalation.ipynb     # Transformer ablation study
├── LICENSE                         # Apache 2.0 License
└── README.md                       # This file
```

## Contributing

Contributions are welcome! Areas for improvement:
- Additional model architectures (e.g., Graph Neural Networks)
- More datasets
- Extended evaluation metrics (e.g., pseudoknot prediction)
- Optimization techniques
- Visualization enhancements

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Citation

If you use this benchmarking suite in your research, please cite:

```bibtex
@software{rna_structure_benchmarking,
  title = {Benchmarking of RNA Secondary Structure Prediction Models},
  author = {programophile},
  year = {2024},
  url = {https://github.com/programophile/Benchmarking-of-RNA-second-structure-prediction-models}
}
```

## Acknowledgments

- **Dataset**: bpRNA-new dataset from [multimolecule](https://huggingface.co/datasets/multimolecule/bprna-new)
- **trRosettaRNA**: Implementation based on [trRosettaRNA2](https://github.com/quailwwk/trRosettaRNA2)
- Deep learning frameworks: PyTorch team

## Contact

For questions, issues, or suggestions, please open an issue on GitHub.

---

**Note**: This is a research and educational project. For production use cases, consider domain-specific optimizations and validations.
