# Intent Analysis

This repository contains a Jupyter Notebook-based project for exploring mechanistic interpretability in language models. The work focuses on using [TransformerLens](https://github.com/neelnanda-io/TransformerLens) with GPT-2 to inspect and analyze internal activations, attention patterns, and steering behavior for code-related prompts.

## Project Overview

The notebook in this repository investigates how a transformer model processes information internally by:

- installing and setting up the required machine learning libraries;
- attaching hooks to model layers to inspect residual stream activations;
- analyzing logit differences for secure vs. insecure code-related completions;
- applying activation steering techniques to influence model behavior;
- studying attention pattern shifts across layers;
- visualizing intermediate representations and model internals.

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

3. Install the required dependencies:
   ```bash
   pip install -U pip
   pip install torch transformers transformer_lens einops numpy matplotlib plotly jupyter
   ```

4. Open the notebook:
   ```bash
   jupyter notebook
   ```

5. Open `MechInterp.ipynb` and run the cells sequentially.

## Notes

- The notebook uses GPT-2 small (`gpt2-small`) and the TransformerLens library for internal model inspection.
- Some cells may require GPU support for faster execution, but CPU execution is also possible.
- The project is designed as an exploratory notebook rather than a packaged Python module.

## Purpose

This repository serves as a hands-on example of mechanistic interpretability research, combining model inspection, activation analysis, and interpretability visualizations in a single workflow.
