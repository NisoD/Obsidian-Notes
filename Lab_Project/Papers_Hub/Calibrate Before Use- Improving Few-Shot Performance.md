---
Year: 2021
Link: https://arxiv.org/pdf/2102.09690
Status: To read
---
# Calibrate Before Use: Improving Few-Shot Performance of Language Models

## Key Problem
- LMs like GPT-3 show high variance in few-shot learning based on:
 - Training example selection 
 - Example ordering
 - Prompt format
- Simple prompt changes can cause 40%+ accuracy swings

## Root Causes
Three main biases identified:
1. Majority label bias - favors frequent prompt labels
2. Recency bias - prefers recent example labels  
3. Common token bias - defaults to common pretrained outputs

## Solution: Contextual Calibration
- Uses "content-free" inputs (e.g. "N/A") to measure bias
- Adjusts output distribution to counteract biases
- Results:
 - Up to 30% accuracy improvement
 - Reduced variance across prompts
 - No additional training needed

## Impact
Makes few-shot learning more reliable and practical for real-world LM applications.