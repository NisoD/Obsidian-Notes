---
Link: https://arxiv.org/pdf/2309.03882v4
Status: To read
---
# Large Language Models Are Not Robust Multiple Choice Selectors

## Key Problem
- LLMs show significant bias in selecting MCQ answers based on option positions (A/B/C/D)
- Changing option order dramatically impacts performance
- Example: Moving answers to position D reduces GPT-3.5-turbo accuracy by 6.3%

## Root Causes
1. Token bias: Inherent preferences for certain option tokens
2. Recency bias: Favoring options presented later in prompt  
3. Majority label bias: Preferring more frequently appearing answers

## Solution: PriDe (Prior Debiasing)
- Estimates model's prior bias using small sample set with permuted options
- Separates bias from overall prediction distribution
- Applies correction to remaining samples 
**Results:**
 - Accuracy improvement up to 30%
 - More consistent cross-position performance
 - Lower computational cost vs full permutation

## Significance
Reveals important robustness issue in LLM MCQ handling while providing efficient bias mitigation without retraining or extensive computation