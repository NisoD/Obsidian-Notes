---
Year: 2023
Brief: "Here you can write a short summary of the paper so you can recall easily what is it about. "
Link: https://arxiv.org/pdf/2401.00595.pdf
Status: Read
Topic:
  - LLM EVAL
---
# Background

Usual benchmark currently uses _single instruction templates_ for evaluation.

**The problem is that this can introduce inconsistency as different phrasing can alter the results for same question**

There is a huge need for multi-prompt eval to asses LLM’s and tailor it for the use case.

# Model

1. Dataset Creation
    1. Automatic generation of prephrased instructions via Chain of Thought prompting.
    2. Manual validation to ensure quality in thousands of templates.
2. Eval setup
    
    1. Eavluate 20 different LLM’s on 39 Tasks from three benchmarks- LMENTRY, Big-Bench Lite & Hard.
    
      
    
3. Metrics for robust eval
    1. **MaxP** - Best performance on single instruction.
    2. **AvgP** - Robustness across all paraphrased instructions.
    3. **Combined Performance Score (CPS)**: Balances both peak performance and consistency.  
          
          
        

# Math

**Kendall’s W:**

![[Attachments/image 17.png|image 17.png]]

$R_i = \sum^{n}_{i=1} r_{i,j}$

Sum of ranks and their mean value

**m** is the instructions | n the judged LLM’s

**Kendall rank correlation coefficient:**

![[Attachments/image 1 10.png|image 1 10.png]]

$M = LLM,T=\{(x_i,y_i)\} \text{eval data set }$

$I_t \text{ set of natural language task instruction paraphrases for T}$

$\epsilon (M,T,i) \in [0,1]$ aggregated(מצטבר) preformarnce of M on samples from T

### MaxP

![[Attachments/image 2 8.png|image 2 8.png]]

  

  

> ==This metric is useful for developers  
> aiming to integrate an LLM into a specific down-  
> stream task and domain (e.g., sentiment analysis in  
> the news domain)  
> ==

### AvgP

![[Attachments/image 3 7.png|image 3 7.png]]

> ==**Use Case**==
> 
> ==Average prompt performance is use-  
> ful for assessing model robustness to paraphrases.  
> ==

### CPS

first we define saturation score to measure peak + robustness

![[Attachments/image 4 5.png|image 4 5.png]]

  

![[Attachments/image 5 3.png|image 5 3.png]]

> This metric is valuable for selecting a model for a suite of applications or a platform offering diverse tasks. For instance, when integrating an LLM into an application with uservisible prompts, such as a multi-functional chatbot, it is crucial for the model to be both effective  
> (high MaxP ) and robust (high Sat).  

# Results

- LLM performance varies drastically across paraphrased instructions.
- Single-prompt evaluations lead to unreliable rankings. For example, models may rank first on one paraphrase and last on another.
- **LLaMA-based models** performed well on best-case prompts but lacked robustness in average performance.
- OpenAI models (like GPT-3.5) also show sensitivity to minor prompt changes.
- Metrics like CPS provide a clearer picture of model reliability and real-world usability.

# AvgP - OpenAI

![[56ebace7-e196-424f-970c-7d87818a4a59.png]]

# MaxP - OpenAI

![[1db73115-5d87-4bc4-b04d-a42679d41bcd.png]]

LLaMA-based models were

![[Attachments/image 6 3.png|image 6 3.png]]

# Code

> [!info] GitHub - SLAB-NLP/Multi-Prompt-LLM-Evaluation: State of What Art? A Call for Multi-Prompt LLM Evaluation  
> State of What Art?  
> [https://github.com/SLAB-NLP/Multi-Prompt-LLM-Evaluation](https://github.com/SLAB-NLP/Multi-Prompt-LLM-Evaluation)  

LMentry Example:

```JSON
{
  "benchmark": "LMentry",
  "task": "all_words_from_category_0_distractors",
  "description": "Task: All words from category\nExample: Q: Are all the words \"chair\", \"bed\", \"table\", \"desk\", and \"sofa\" types of furniture?  Answer either \"yes\" or \"no\".",
  "format": "classification (yes/no)",
  "num_of_instances": 1000,
  "more_info": {
    "num_words_options": [5],
    "num_distractors_options": [0],
    "seed": 1407,
    "input_templates": [
      "Q: Are all the words {words} types of {category}? Answer either \"yes\" or \"no\".\nA:",
      "Q: Do the words {words} all represent {category}? Answer either \"yes\" or \"no\".\nA:",
      "Q: Does the list [{words}] contain only {category}? Answer either \"yes\" or \"no\".\nA:"
    ]
  },
  "examples": {
    "1": {
      "words": ["rabbit", "dog", "goat", "cat", "duck"],
      "category": "animals",
      "gold": "yes",
      "more_info": {
        "num_words": 5,
        "category_words": ["rabbit", "dog", "goat", "cat", "duck"],
        "distractors": [],
        "num_distractors": 0,
        "distractor_indices": []
      }
```

BBH

```JSON
  "benchmark": "big_bench_hard",
  "task": "causal_judgement",
  "format": "classification (yes/no)",
  "task_type": "nlp",
  "num_of_instances": 187,
  "description": "Answer questions about causal attribution.",
  "more_info": {
    "input_templates": [
      "Q: How would a typical person answer each of the following questions about causation?\n{question}\nOptions:\n- Yes\n- No\nA:"
    ],
    "key_names": ["question"],
    "few_shot_examples": {
      "0": {
        "question": "Frank T., had an ongoing dispute with his neighbor over a stretch of land and one day decided to shoot his neighbor in the body. Frank T. had no experience with guns, his hand slipped on the barrel of the gun, and the shot went wild. Nonetheless, the bullet bounced off a large boulder several feet away and hit the neighbor's body, causing significant injury. Did Frank T. intentionally shoot his neighbor in the body?",
        "gold": "No",
        "explanation": "Here in this question, we are told that \"Frank T. had no experience with guns, his hand slipped on the barrel of the gun, and the shot went wild.\" A typical person would assume that this passage suggests that Frank T. had no intention of shooting and injuring someone and that the bullet accidentally hit the neighbor's body; therefore, we conclude that Frank T. did not intentionally hit his neighbor. So the answer is No."
      },
      "1": {
        "question": "Suzy and Billy are working on a project that is very important for our nation's security. The boss tells them both",
        "gold": "Yes",
        "explanation": "Here in this question, we are told that the boss ordered them both to arrive at the meeting room at the same time and that the motion detector was set up to be triggered if at least one person appeared in the room at the same time.\" A typical person would assume that the person probably meant to say the detector was set up to be triggered if \"both persons\" appeared in the room at the same time, not at least one person, since otherwise the phrase \"at the same time\" would not make much sense in that sentence. Because the motion detector went off, a typical person would therefore come to the conclusion that both Suzy and Billy triggered the motion detector to go off; hence, Billy did indeed cause the motion detector to go off. So the answer is Yes."
    
```