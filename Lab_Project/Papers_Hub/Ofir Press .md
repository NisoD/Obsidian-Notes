---
Status: To read
---
# Background

> Language models (LMs) are increasingly used to assist users in day-to-day tasks such as programming (e.g., GitHub Copilot) or search (e.g., Google's AI Overviews).  
> But can we build language model systems that are able to autonomously complete entire tasks end-to-end?  

In this talk, I'll discuss our efforts to build autonomous LM systems, focusing on the software engineering domain.  
I'll present **SWE-bench**, our novel method for measuring the performance of automatic programming systems on their ability to fix real issues in popular software libraries from GitHub.  

I'll then introduce **SWE-agent**, our system for solving SWE-bench tasks.  

**SWE-bench** and **SWE-agent** are used by many leading AI organizations in academia and industry, including OpenAI, Anthropic, Meta, and Google.  
These projects demonstrate that academics on tight budgets can have a substantial impact on steering the research community toward building autonomous systems capable of completing challenging tasks.

---

## Key Challenges

### 1. The Problem with Attention: Human Bias Toward Closeness  
Language models often exhibit a **bias toward proximity** when processing sequences. To address this:  

- **Alibi Attention**:  
  Reduce the attention score proportionally to the distance between words:  
  $$ alibi_{attention} $$  

  [Read the paper on Alibi Attention](https://arxiv.org/pdf/2108.12409).

---

### 2. Benchmark Construction: Striking the Right Balance  
Creating effective benchmarks for autonomous systems is challenging:  

- **State-of-the-Art (SoTA) Models**:  
  These models often achieve maximum scores (minus human error), but:  
  - **Constructing challenging benchmarks** is relatively easy.  
  - **Validating these benchmarks** is much harder.

#### Our Goals for Benchmarks:
1. **Challenging**  
2. **Easy to Validate**  
3. **Natural and Useful**

#### Example:
The selected topic is **software engineering automation**.  

- **Question**: A bug report.  
- **Answer**: The solution to the code problem.  

**Issue**:  
Coding isn’t deterministic, and there are many ways to solve a bug.  

> **LLMs as Judges**: LLMs tend to be biased toward their own generated solutions.  

---

## Evaluation Approach

**How did we evaluate model performance?**  
We submitted the model's pull requests (PRs) to repositories and:  
- Tested them by running **all unit tests** in the repository.  

**Statistics:**  
- Average repository size: **400k lines of code**.
- We achieved **12.5** performance on open source model.
[Paper of SWE-Agent](https://arxiv.org/pdf/2405.15793)
## Problems we faced
1) First hurdle, was to take a model that was trained for instructions and make it work in its own environment where it can interact with the computer freely and has to do so efficiently.
Possible solution - create a new GUI for the agent:
- build a new program to view files that takes a huge file and chunks it
2) The second hurdle was that models had hard time specifing the relevant lines for changing.
Possible solution - Add a linter that checks that the code syntax is correct when editing if not it won't apply and show the linting error.

---
