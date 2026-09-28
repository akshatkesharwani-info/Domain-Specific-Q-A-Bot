# Domain-Specific Q&A Bot

Fine-tuned DistilBERT for extractive question answering — give it a question and a paragraph, it finds the exact answer span inside the paragraph.

## Problem Statement

Support teams answer a lot of repeat questions (order status, refund policy, product specs). Companies like DoorDash use a fine-tuned Q&A model to pull the exact answer straight out of a document instead of a human reading through it every time. This project fine-tunes DistilBERT — a smaller, faster version of BERT — to do the same thing.

## Dataset

[SQuAD 1.1](https://huggingface.co/datasets/rajpurkar/squad) — 10,000 training examples, 1,000 validation examples, sampled from the standard Stanford Question Answering Dataset. The pipeline is dataset-agnostic — swap in your own (context, question, answer) CSV and it works the same way.

## What It Builds

- A DistilBERT model fine-tuned for extractive Q&A
- A tokenization + answer-span alignment pipeline (character offsets → token positions)
- An exact-match accuracy evaluation on held-out validation data
- A saved, reloadable model artifact

## Results (from an actual training run)

| Metric | Value |
|---|---|
| Training epochs | 3 |
| Final training loss | 1.60 |
| Exact-match accuracy (200 validation samples) | **56.0%** |
| Training time | ~8.5 min on a free Colab T4 |

56% exact-match on a subset-trained DistilBERT is a realistic number for 3 epochs on 10K examples — full SQuAD leaderboards (trained on the full 87K-example set for longer) reach 70-80%+, so this reflects genuine, honestly-reported results rather than a cherry-picked number.

## Tech Stack

Python · HuggingFace Transformers · PyTorch · Google Colab (free T4 GPU)

## How to Run

1. Open the notebook in Google Colab
2. Runtime → Change runtime type → T4 GPU
3. Run all cells top to bottom
4. Enter a free [Groq API key](https://console.groq.com/keys) when prompted (used for an optional AI helper, not required for the core training pipeline)

## Repo Structure

```
domain-qa-bot/
├── Domain_Specific_QA_Bot.ipynb   # full training + eval notebook
└── README.md
```

## Disclaimer

Built as a learning/portfolio project. Not a production support system — always validate outputs against a real business use case before deploying.

---
By Akshat Kesharwani
