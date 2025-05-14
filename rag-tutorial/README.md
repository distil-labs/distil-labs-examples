# RAG‑Roman‑Empire — Quick Start

This repo contains a **step‑by‑step Jupyter notebook** that shows you how to:

1. **Spin up a baseline Retrieval‑Augmented Generation (RAG) prototype** for answering questions about the Roman Empire using a small open‑source chat model, vLLM, and a Wikipedia article as the knowledge base.
2. **Fine‑tune that model with the distil labs platform**—upload a tiny QA dataset, evaluate a teacher LLM, and distil its knowledge into a 135 M‑parameter student.
3. **Redeploy the tuned weights locally** and drop them into the same RAG loop for higher‑accuracy answers on commodity hardware.

## Folder layout

```
.
├─ rag-tutorial.ipynb       # Main notebook (three chapters)
├─ data/                    # Job description, train/test, unstructured docs
├─ readme.md                # (this file)
└─ model/                   # Populated after distil‑labs training download
```

## Prerequisites

* Python 3.10+
* `pip install vllm langchain-core langchain_community langchain-openai langchain-huggingface wikipedia pandas requests rich pyyaml`
* A **distil labs** account for fine‑tuning

## One‑line demo

```bash
python -m vllm.entrypoints.openai.api_server \
    --model HuggingFaceTB/SmolLM2-135M-Instruct --device cpu &
```

Then open the notebook and run Chapter 1 to play with the baseline RAG loop.

Happy hacking!
