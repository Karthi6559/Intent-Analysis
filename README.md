# Intent Analysis

This repository contains a Jupyter Notebook-based project for exploring mechanistic interpretability in language models. The work focuses on using [TransformerLens](https://github.com/neelnanda-io/TransformerLens) with GPT-2 to inspect and analyze internal activations, attention patterns, and steering behavior for code-related prompts.

## Project Overview

The notebook in this repository investigates how a transformer model processes information internally by:

- Find out the layer that is causing the activation.
- Perform Intervention of the Layer.
- Try the same thing on MLM (Medium language model)

This work is framed around mechanistic interpretability and is intended as a practical exploration of how internal model components contribute to behavior.

## Repository Structure

- `MechInterp.ipynb` – main notebook containing the experiment pipeline and analysis.
- `MechInterp_executed.ipynb` – executed version of the notebook with outputs preserved.
- `dataset/vibecheck_dataset.json` – dataset file included in the repository.
- `README.md` – project overview and usage instructions.

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/Karthi6559/Intent-Analysis.git
   cd Intent-Analysis
   ```

2. Create and activate a Python environment (recommended):
   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```
4.  Open the notebook:
   ```bash
   jupyter notebook
   ```
   
3. Install the required dependencies:
   ```bash
   pip install -U pip
   pip install torch transformers transformer_lens einops numpy matplotlib plotly jupyter
   ```
   
5. Open `MechInterp.ipynb` and run the cells sequentially.


## Purpose

This repository serves as Intent analysis framework for figuring out security threats that are produced by prompt engineering.
