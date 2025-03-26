---
Link: https://aclanthology.org/2024.lrec-main.1229.pdf
Status: To read
---
# Self-Consistency Challenges in LLM Multiple Choice Question Evaluation

## Key Problem
- LLMs show inconsistent answers when same question presented differently
- Accuracy varies significantly with:
 - Option position shuffling 
 - Label changes (A/B/C/D vs emoji symbols)
 - Format changes (MCQ vs True/False)
- Example: Platypus2-13b accuracy drops 57.1% → 37.6% with question variants

## Methods
Three consistency test variants:
1. Option position shuffle - Rearrange answer choices
2. Label replacement - Replace A/B/C/D with emoji symbols 
3. True/False format - Convert MCQ to judgment questions

## Key Findings

### Model Size Impact
- Larger models (>30B) show better consistency
- Small models (<13B) highly sensitive to variants
- Parameter scaling improves robustness

### Training Impact
- SFT and RLHF models more consistent than base PLMs
- At 13B: SFT/RLHF outperform PLMs on consistency metrics
- RLHF shows particular stability across variants 

### Rankings Impact
- Model rankings shift significantly under different formats
- 7B/13B models especially sensitive to evaluation changes
- Questions reliability of current leaderboard methodologies

## Significance
Authors propose consistent accuracy as more reliable metric for MCQ evaluation, revealing important robustness gaps in current LLM evaluation methods.