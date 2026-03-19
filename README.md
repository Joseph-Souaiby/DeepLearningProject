# Detecting LLM-Generated Student Essays with Transformer Fine-Tuning and Robustness Analysis

**Joseph Souaiby & Huzaifah Wasim**

The rapid improvement of large language models (LLMs) has made machine-generated writing increasingly fluent, raising practical concerns for academic integrity, misinformation, and platform trust. While early detectors often relied on shallow cues or perplexity-based heuristics, modern systems must remain accurate under distribution shifts, such as changes in topic, writing style, or the underlying generator model. Our project studies trained AI-text detectors in a realistic setting: distinguishing student-written essays from LLM-generated essays, with an explicit emphasis on robustness beyond a single dataset.

We frame the task as binary text classification. The input is an essay (raw text), and the output is a probability that the essay was AI-generated. We will train and compare (i) classical feature-based baselines and (ii) transformer-based classifiers built on pre-trained encoders such as BERT/RoBERTa. Beyond reporting accuracy on held-out data, we will analyze generalization to out-of-domain (OOD) sources and unseen generators, and we will study what statistical cues the model exploits, informed by prior work on human-interpretable detection signals.

## Setup

This project uses [uv](https://docs.astral.sh/uv/) for Python environment management.

### Install uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Install dependencies

```bash
uv sync
```

### Run the notebook

```bash
uv run jupyter notebook TFIDF.ipynb
```

### Add or remove packages

```bash
uv add <package-name>
uv remove <package-name>
```
