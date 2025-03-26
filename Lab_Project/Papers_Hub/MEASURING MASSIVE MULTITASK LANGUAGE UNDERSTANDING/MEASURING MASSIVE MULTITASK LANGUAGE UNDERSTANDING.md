---
Year: 2020
Brief: These brief summaries can also be useful if you are working in a team or running a journal club where different members read and present papers. This way all of the team can read the brief summary.
Status: Read
Topic:
  - LLM EVAL
PDF:
  - "[[MMLUNotes.pdf]]"
---
# MMLU Paper Summary

## Evaluation Methods

- 5-shot evaluation with demonstration examples
- Models predict A/B/C/D options based on highest probability
- Fixed dev set with 5 examples per subject

## Key Findings

- Model size directly impacts performance
- Fine-tuning improves results vs few-shot learning
- Calibration issues exist in large neural networks
- UnifiedQA shows advantages due to QA dataset fine-tuning

## Future Directions

1. Multimodal Understanding

- Proposed "Turk Test" using Mechanical Turk tasks
- Focus on flexible formats and multimodal inputs

1. Training Methodology

- Shift toward human-like learning (books, discussions)
- Example: Legal domain has vast corpora but limited practice questions
- Need for better pretraining approaches

## Experimental Results

- RoBERTa-base results:
    - 32.8% accuracy with 2,000 law examples
    - 36.1% accuracy after pretraining on 1.6M legal cases
- Indicates scaling alone may not solve performance issues

## Implications

- Models need better learning approaches beyond question banks
- Additional pretraining helps but has diminishing returns
- Current architectures may need fundamental improvements