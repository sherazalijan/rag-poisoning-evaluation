# RAG Poisoning Evaluation

A controlled experimental study investigating the vulnerability of Retrieval-Augmented Generation (RAG) systems to document poisoning.

## Overview

This project evaluates whether semantically relevant but untrusted documents can enter a RAG retrieval pipeline and influence the final generated response.

The experiment uses a controlled corpus containing both trusted and intentionally poisoned documents. Questions are evaluated using semantic retrieval followed by LLM generation.

## Objective

The main objectives are to:

- Measure how frequently poisoned documents enter the retrieved context.
- Determine whether retrieved poisoned information is adopted by the language model.
- Establish a reproducible baseline for evaluating RAG poisoning resistance.
- Provide a foundation for testing defenses such as source-trust filtering.

## Experimental Setup

The experiment uses:

- Sentence-Transformer embeddings
- FAISS similarity search
- Top-k semantic retrieval
- Gemini-based generation
- Trusted and untrusted document sources
- 40 evaluation questions

### Conditions

The evaluation is structured around:

1. **Clean RAG** — trusted documents only
2. **Poisoned RAG** — trusted + untrusted documents
3. **Defended RAG** — poisoned corpus with source-trust filtering

## Current Results

### 40-Question Poisoned RAG Baseline

| Metric | Result |
|---|---:|
| Evaluation questions | 40 |
| Poisoned document retrieval | 39/40 |
| Retrieval exposure | **97.5%** |
| Poisoning adoption | **0/40** |
| Poisoning success rate | **0%** |

The baseline demonstrates that poisoned documents can enter the retrieval context at a high rate, while the evaluated model did not adopt the poisoned claims under the current attack configuration.

## Metrics

### Retrieval Exposure Rate

The percentage of questions for which at least one untrusted document appears in the retrieved context.

\[
\text{Retrieval Exposure} =
\frac{\text{Questions with poisoned retrieval}}
{\text{Total questions}}
\times 100
\]

### Poisoning Success Rate

The percentage of questions for which the model actually adopts information from a poisoned document.

\[
\text{Poisoning Success} =
\frac{\text{Questions where poisoned information is adopted}}
{\text{Total questions}}
\times 100
\]

## Project Structure

```text
rag-poisoning-evaluation/
│
├── notebook.ipynb
├── rag_poisoning_40_results.csv
├── rag_poisoning_summary.csv
├── successful_poisoning_cases.csv
├── rag_poisoning_results.png
└── README.md
