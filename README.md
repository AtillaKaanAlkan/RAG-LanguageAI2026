# 🔭 UAT Keyword Assignment: Zero-Shot vs Few-Shot vs RAG

> A tutorial comparing three LLM-based approaches to automatically assign [Unified Astronomy Thesaurus (UAT)](https://astrothesaurus.org) keywords to astronomical abstracts.

[![Dataset](https://img.shields.io/badge/🤗%20Dataset-SciX%20UAT%20Keywords-blue)](https://huggingface.co/datasets/adsabs/SciX_UAT_keywords)
[![Model](https://img.shields.io/badge/LLM-DeepSeek--Reasoner-green)](https://api.deepseek.com)
[![NASA ADS](https://img.shields.io/badge/NASA-ADS%20%2F%20SciX-red)](https://ui.adsabs.harvard.edu)

---

## Overview

This tutorial notebook **`uat_rag_tutorial.ipynb`** demonstrates three progressively more powerful approaches to UAT keyword assignment:

| Approach | Core idea | Data needed | Infrastructure |
|---|---|---|---|
| 🔵 **Zero-Shot** | Ask the LLM directly, no examples | None | None |
| 🟠 **Few-Shot** | Include a few labeled examples in the prompt | A handful | None |
| 🟢 **RAG** | Dynamically retrieve the most similar labeled abstracts | Large corpus | Embedding model + vector DB |

If you want to learn more about Retrieval-Augmented Generation (RAG) before starting this tutorial, you can read this [post](https://github.com/AtillaKaanAlkan/retrieval-augmented-generation).

---

## Motivation

The UAT is a controlled vocabulary of 2,000+ standardized astronomy concepts used by NASA ADS to index the scientific literature. Assigning these keywords manually is time-consuming. This tutorial explores how far LLMs can take us — and whether grounding them in a retrieval system makes a meaningful difference.

---

## Dataset

We use the [SciX UAT Keywords](https://huggingface.co/datasets/adsabs/SciX_UAT_keywords) dataset:

- **18,677** training abstracts with verified UAT labels
- **3,025** validation abstracts
- Each abstract comes with `bibcode`, `title`, `abstract`, and `verified_uat_labels`

Labels correspond to authors assigned keywords.

---

## Quickstart

```bash
# 1. Clone the repo
git clone https://github.com/AtillaKaanAlkan/RAG-LanguageAI2026.git
cd RAG-LanguageAI2026

# 2. Create a virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add your DeepSeek API key
echo "deepseek_api_key=copy_paste_your_key_here" > .env

# 5. Launch the notebook
jupyter notebook uat_rag_tutorial-v2.ipynb
```

---

## Repository Structure

```
uat-rag-tutorial/
├── uat_rag_tutorial-v2.ipynb   # Main tutorial notebook
├── requirements.txt
├── .env                     # Your API key (never committed)
├── .gitignore
└── README.md
```

---

## Evaluation Metrics

We evaluate each approach using **ranked metrics** designed for multi-label classification:

- **P@k** — Precision at k: fraction of top-k predictions that are correct
- **R@k** — Recall at k: fraction of correct labels found in top-k predictions  
- **F1@k** — Harmonic mean of P@k and R@k

Evaluated at k ∈ {1, 3, 5, 10}.


---

*Built By Atilla Alkan @ Harvard-Smithsonian Center for Astrophysics / [NASA ADS](https://ui.adsabs.harvard.edu)*