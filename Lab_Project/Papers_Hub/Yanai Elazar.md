---
Status: To read
---
# Background

### Models are biased and hallucinate lets build our trust 
Three steps :
- Model interpertability
- Data collections and analysis
- models as data storers
## Model interpretability
Probing - isnt the initial task but we can see that the model can derive it 
How can we investigate the causal effect of a property has on the output 
( Putting nurse instead of scientist )
[Paper](https://arxiv.org/pdf/2006.00995)
## Data Handling in training to achieve SOTA Model
In recent years we saw the rise of open source AI models
Moreover, we beleive in data accessability we want to be able to asses the amount of examples there was seen during training to understand the performance of the model
[Paper](https://arxiv.org/abs/2310.20707)
[Code](https://github.com/allenai/wimbd)
## Understanding Models through data
Can we find a number which will be sufficent enough to imitate that in a response
[Paper](https://arxiv.org/pdf/2410.15002)
In order to anwser this question we should train many models that vary only in the amount of mentions of the specific topic (i.e Leonardo dicapprio) 
*This is very expensive to train*

Another approach is collecting number of occournces of each topic and scoring it according to the number of times it appears.
Overall imitation threshold 100-650 images
Different topics have differing variance as imitations will require more .
[Used Model](https://laion.ai/blog/laion-400-open-dataset/)
> If we can understand the data we can understand the model and by knowing the amount of examples that it has seen we can derive from it whether it will be able to imitate the work of others and be problematic in respect to Copy Rights

As the organizations won't let us into their black box solution we need to derive and reverse engineer via checking the ability to imitate 

- open question :
	to understand the impact of the data we have to understand the impact of each segment in out architecture on the output
	
# Model

Add text here

# Results

Add text here

# Code

Add link to code here (if exists)