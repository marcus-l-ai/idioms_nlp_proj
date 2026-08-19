# Idioms NLP Project

Fine-tuning **Google FLAN-T5-Large** to understand and generate English idioms from contextual examples.

## Overview

Idioms are difficult for language models because their meaning often cannot be inferred literally from the individual words. This project explores whether a sequence-to-sequence language model can learn idiomatic meaning from context.

The project fine-tunes `google/flan-t5-large` on an idiom dataset and evaluates two related tasks:

1. **Idiom interpretation** — given an idiom and a sentence containing it, explain what the idiom means in context.
2. **Idiom generation** — given an idiom's meaning and a scenario, generate an appropriate idiom and sentence.

### Key Files

* **`dataset/idioms_dataset.csv`** — formatted idiom training and evaluation data.
* **`data_prep.ipynb`** — prepares and cleans the source datasets.
* **`flan_t5_large_model.ipynb`** — main FLAN-T5-Large fine-tuning pipeline.
* **`flan_t5_large_eval.ipynb`** — evaluates the fine-tuned model.
* **`outputs/flan-t5-large-idiom-combined/`** — saved fine-tuned model.
* **`custom_generation_results.csv`** — generated predictions from custom examples.
* **`idioms BERTScore.txt`** — recorded BERTScore evaluation results.
* **`model_performance_comparison.png`** — model performance visualization.

## Tasks

### 1. Idiom Interpretation

The model receives an idiom and a sentence containing it and generates an explanation of its meaning.

**Input:**

```text
Idiom: same difference
Sentence: With a beard, without a beard, same difference.
```

**Expected output:**

```text
Same difference means the distinction makes no practical difference.
```

### 2. Idiom Generation

The model receives an idiom's meaning and a scenario and attempts to generate the appropriate idiom.

**Input:**

```text
Meaning: [IDIOM] means the distinction makes no practical difference.
Scenario: With a beard, without a beard, it amounts to the same thing.
```

**Expected output:**

```text
Idiom: same difference
Sentence: With a beard, without a beard, same difference.
```

This multi-task approach allows the model to learn both **understanding idioms** and **using idioms in context**.

## Results

The fine-tuned model can produce semantically relevant explanations for many familiar idioms.

For example, when given **"turn over a new leaf,"** the model generated an interpretation describing the idea of beginning a new and improved course of action.

However, idiom generation is more challenging. The model sometimes generates an idiom that is semantically related to the scenario but is not the intended expression. This indicates that the model can capture aspects of an idiom's meaning without always retrieving the exact idiom.

## Limitations

* The training dataset is relatively small for fine-tuning a large language model.
* BERTScore measures semantic similarity but does not guarantee correct idiom interpretation.
* Idiom generation can produce plausible but incorrect expressions.
* The project is primarily notebook-based rather than packaged as a reusable Python application.
* Training uses a small batch size and is intended primarily as an experimental NLP project.