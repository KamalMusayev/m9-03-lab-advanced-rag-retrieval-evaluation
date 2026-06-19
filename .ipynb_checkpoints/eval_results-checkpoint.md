# Retrieval Evaluation Results

## Overview

This evaluation compares the original dense retrieval approach from Lab 2 with the improved hybrid retrieval approach.

The baseline system uses only semantic search with Chroma embeddings.

The upgraded system combines:

- Dense retrieval using vector similarity
- BM25 keyword retrieval for exact term matching

Both systems use the same generation model and prompt. The only difference is the retrieval strategy.

---

## Evaluation Dataset

The evaluation set contains 5 questions from the knowledge base.

Each question is mapped to the expected passage id that should be retrieved.

| Question | Expected Passage |
|---|---|
| What does error 0x80070005 mean? | kb-08 |
| How do I reset my password? | kb-07 |
| How can I cancel my subscription? | kb-05 |
| How long do I have to get a full refund? | kb-04 |
| When is the office kitchen restocked? | kb-10 |

The evaluation includes an exact technical term (`0x80070005`) to test keyword-based retrieval performance.

---

## Metrics

### Retrieval Hit Rate

Retrieval hit rate measures whether the expected passage id appears in the retrieved documents.

No LLM is used for this metric. It is an exact comparison between the retrieved ids and the expected id.

### Faithfulness

Faithfulness is evaluated using an LLM-as-judge approach.

The judge checks whether the generated answer is fully supported by the retrieved context.

The result is classified as:

- YES → answer is supported by context
- NO → answer contains unsupported information

---

## Results

| System | Retrieval Hit Rate | Faithfulness |
|---|---:|---:|
| Dense Baseline | 1.0 | 0.6 |
| Hybrid Retrieval | 1.0 | 0.8 |

---

## Conclusion

The hybrid retrieval approach did not improve retrieval hit rate on this evaluation set because the dense retriever already retrieved all expected passages correctly.

However, hybrid retrieval improved faithfulness from 0.6 to 0.8, suggesting that combining semantic search with BM25 keyword matching provided better context for answer generation.

The results show why retrieval improvements should be measured with evaluation metrics instead of assumptions.