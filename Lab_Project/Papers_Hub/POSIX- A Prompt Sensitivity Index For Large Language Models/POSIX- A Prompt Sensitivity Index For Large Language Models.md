---
Year: 2024
Brief: The goal of this brief is to allow future-you to skim over all the papers you’ve read for a specific research or about a specific topic.
Link: https://arxiv.org/pdf/2410.02185.pdf
Status: Read
Topic:
  - LLM EVAL
---
# Background

  

**performance spread** – defined as the difference between the highest and lowest average

performances observed across a wide range of prompt templates – and used this as a surrogate for prompt sensitivity

  

# Intro

we must distinguish between

response distribution matters: a model producing a consistent response in all but one case  
is less sensitive than one generating two different responses - each equally frequent.  

**Four key factors when evaluating that indicate higher sensetivity**

1. **response diversity** - Higher number of unique response
2. **Response Distribution Entropy** - Higher entropy of unique response appearing
3. **Semantic Coherence** - lower semantic similarity amongsts awnsers
4. **Variance in confidence**- higher variance in log-likelihood of same response  
      
    

![[Attachments/image 16.png|image 16.png]]

> If the intent of the prompts is the same, a **consistent LLM** should give responses with similar likelihoods, no matter how you reword the prompt.  
>   

# Math

ר

![[Attachments/image 1 9.png|image 1 9.png]]

![[Attachments/image 2 7.png|image 2 7.png]]

![[Attachments/image 3 6.png|image 3 6.png]]

Senestivity part explained

- look at all pairs of prompts with similar meaning
- compare the probability of receving the same outputs and responses for each pair
- Normlazing vs length so longer prompts dont get more weight

![[Attachments/image 4 4.png|image 4 4.png]]

Same but for the whole dataset

_important remark_

![[Attachments/image 5 2.png|image 5 2.png]]

![[Attachments/image 6 2.png|image 6 2.png]]

# Expirment

- **Models Studied**:
    - Families: **LLaMA**, **Mistral**, and **OLMo**.
    - Models include:
        - LLaMA-2 7B (base & chat), LLaMA-3 8B (base & instruct).
        - Mistral 7B (base & instruct).
        - OLMo 7B (base & instruct).
- **Datasets**:
    - **MMLU**: Benchmark for multi-choice tasks (~14,000 prompts from 57 domains).
    - **Alpaca**: Open-ended generation tasks (5,000 sampled prompts).
    - **BBH**: Additional dataset in Appendix E.
- **Prompt Variations**:
    - **Spelling Errors**: Random token modifications (insertion, omission, transposition, substitution) on 1, 2, 4, or 8 tokens.
    - **Prompt Templates**: 20 templates designed to alter the structure but retain meaning.
    - **Paraphrasing**: 20 reworded prompts using GPT-3.5-Turbo.
    - **Mixture**: Uniform sampling of 21 prompts across the three variation types.
- **POSIX Calculation**:
    - For each prompt, POSIX is calculated using the original prompt and its **20 variants**.
    - **MMLU**: Outputs 5 tokens (MCQ tasks).
    - **Alpaca**: Outputs 30 tokens (open-ended tasks).
    - POSIX is normalized by token count, ensuring comparability across output lengths.
- **Results**:
    - infer that increase in paramteter count does not neccessarily decresase prompt sensitivity.
    - Adding few shot examplers can significantly reduce prompt sensitivity
    - Mutliple Choice Question is most sensetive for variation  
        refining and getting the **proper prompt template**
    - For open questions **re-phrase** or **reword** the query properly  
          
        

# Paper Explained

  

[https://youtu.be/WV1hfWmIAIM](https://youtu.be/WV1hfWmIAIM)

# Code

https://github.com/kowndinya-renduchintala/POSIX

[https://arxiv.org/pdf/2410.02185](https://arxiv.org/pdf/2410.02185)

![[Attachments/image 7 2.png|image 7 2.png]]