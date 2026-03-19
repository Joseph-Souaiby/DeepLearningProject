# Detecting LLM-Generated Student Essays with Transformer Fine-Tuning and Robustness Analysis

**Joseph Souaiby & Huzaifah Wasim**

The rapid improvement of large language models (LLMs) has made machine-generated writing increasingly fluent, raising practical concerns for academic integrity, misinformation, and platform trust. While early detectors often relied on shallow cues or perplexity-based heuristics, modern systems must remain accurate under distribution shifts, such as changes in topic, writing style, or the underlying generator model. Our project studies trained AI-text detectors in a realistic setting: distinguishing student-written essays from LLM-generated essays, with an explicit emphasis on robustness beyond a single dataset.

We frame the task as binary text classification. The input is an essay (raw text), and the output is a probability that the essay was AI-generated. We will train and compare (i) classical feature-based baselines and (ii) transformer-based classifiers built on pre-trained encoders such as BERT/RoBERTa. Beyond reporting accuracy on held-out data, we will analyze generalization to out-of-domain (OOD) sources and unseen generators, and we will study what statistical cues the model exploits, informed by prior work on human-interpretable detection signals.

## Setup

This project uses [uv](https://docs.astral.sh/uv/) for Python environment management.

### 1. Install uv

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

After installation, restart your terminal (or run `source $HOME/.local/bin/env`) so that the `uv` command is available.

### 2. Clone the repository

```bash
git clone <repo-url>
cd DeepLearningProject
```

### 3. Install dependencies

This creates a `.venv` virtual environment and installs all packages from `pyproject.toml`:

```bash
uv sync
```

### 4. Run the notebook

```bash
uv run jupyter notebook TFIDF.ipynb
```

This launches Jupyter in your browser with the project's virtual environment automatically activated.

### Add or remove packages

```bash
uv add <package-name>
uv remove <package-name>
```

These commands update both `pyproject.toml` and the lockfile. Run `uv sync` after pulling changes from teammates to stay in sync.
