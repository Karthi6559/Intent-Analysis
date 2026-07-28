# Intent Analysis

This repository explores mechanistic interpretability of language models using
[TransformerLens](https://github.com/neelnanda-io/TransformerLens), asking a specific question:
does a model's internal preference for *secure* vs. *insecure* code change based on how a request
is framed, rather than what is actually asked?

The benchmark centers on a single flagship scenario — a Terraform `aws_s3_bucket_acl` resource
whose `acl` value diverges between `"private"` (secure) and `"public"` (insecure) — rewritten
structurally and paired with different stated intents, then run through the same interpretability
pipeline on two models side by side.

## Repository Structure

- `MechInterp_better.ipynb` – benchmarking pipeline for **GPT-2-small** (12 layers, ~124M params).
- `MechInterp_better _Qwen.ipynb` – the same pipeline for **Qwen2.5-1.5B-Instruct** (28 layers).
- `dataset/Intent_Based_Data.json` – the 20-entry benchmark dataset (see below).
- `intent_benchmark_table.csv` – latest per-scenario benchmark-table output.
- `intent_per_scenario_benchmark.png` – per-scenario logit-lens / DLA plots.
- `intent_batch_summary.png` – aggregate baseline logit diff and peak-layer distribution.
- `intent_head_vs_mlp.png` – summed attention-head vs. MLP contribution, per scenario.
- `README.md` – this file.

## Dataset

`dataset/Intent_Based_Data.json` holds 20 paired scenarios, all built around the same flagship
`aws_s3_bucket_acl` resource, crossed along two axes:

- **`variation_axis`** (4 values) — a structural/syntactic rewrite of the same resource block:
  `naming`, `bucket_ref`, `formatting`, `context_distance`.
- **`type` / `type_label`** (5 values, A–E) — an intent framing prepended via `intent_prefix`:
  secure-stated, neutral, explicit directive, persona-driven, remediation-framed.

Every entry also carries `cwe` (`CWE-732` — Incorrect Permission Assignment for Critical Resource,
for all 20 entries) and `taxonomy_label` (e.g. `"Secure Intent, Insecure Output"`), describing the
relationship between stated intent and code behavior that framing is designed to test.

## Benchmarking Pipeline

Both notebooks run the same four techniques on every scenario:

1. **Baseline logit diff** — given only the shared context, does the model already prefer the
   secure token over the insecure one, before any intervention?
2. **Logit lens** — layer by layer, does the internal residual stream already encode a secure
   preference, even where the final output doesn't show it?
3. **DLA (direct logit attribution)** — at the layer where the effect is strongest, which
   individual attention heads are pushing toward the insecure token?
4. **MLP DLA** — at that same layer, how does the MLP's own contribution compare in sign and
   magnitude to the summed effect of the attention heads?

Each notebook walks through: Setup → Load the Benchmark Set → The Benchmarking Pipeline → Run the
Benchmark → Benchmark Table → Per-Scenario Comparison → Aggregate Summary → Head-Sum vs. MLP
Contribution Across Scenarios — with closing notes on how to interpret the results.

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
   pip install torch transformers transformer_lens einops pandas matplotlib jupyter
   ```

4. Open a notebook:
   ```bash
   jupyter notebook
   ```

5. Run `MechInterp_better.ipynb` (GPT-2-small — runs comfortably on CPU) or
   `MechInterp_better _Qwen.ipynb` (Qwen2.5-1.5B-Instruct — a 1.5B-parameter model; a GPU or
   Apple-silicon MPS device is recommended) cell by cell. Each notebook downloads its own model
   from Hugging Face on first run and reads `dataset/Intent_Based_Data.json`.

## Purpose

This repository is an intent-analysis framework for studying whether models shift their security
posture based on how a request is framed — i.e., risk introduced not by *what* is asked of a
code-generation model, but by *how* it's asked.
