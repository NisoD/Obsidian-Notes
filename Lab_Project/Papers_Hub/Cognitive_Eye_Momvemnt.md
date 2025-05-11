# Abstarct

Real-Time Decoding of Cognitive State from Eye Movements in Reading with LLMs
When reading, our eyes move over the text in a way that is highly informative about us, the text and how we interact with it. I will present recent work from my lab, where we develop LLMs and other computational models that can decode key aspects of the cognitive state of the reader in real time. These include decoding of information seeking, prior exposure to the text, and one of the holy grails in psycholinguistics, decoding of reading comprehension. I will further discuss how feature and model behavior analysis in the presented tasks can improve our scientific understanding of human language processing.
# Background
How do we track text with our eyes?
-  Saccades - rapid eye jump between words
- Fixation - brief pause and fixation on a word (can inedcate difficulty)
- Regression - Jump back to previous word
## Claim
We are able to predict by eye movement the score on the mcq.

## Data Curation
- Made a MCQ for paragraph reading comprehension + annotation of options according to whether this is a distraction/correct/wrong.

## reading comprehension
The goal is to identify whether a given person was provided a question to answer prior to reading or whether he is reading for overall understanding

# Model
## Data Input approach
- Encode the eye movment + text
- Pre-process them separately and use cross attention
- Integrate and correlate them prior to embedding
> How is eye movement represented?
> Fixation Level, Raw data of XY Cords, total fixation duration
## Used model - RoBERTEye
Combine at input the Eye Projection + word embeddings
Send to LM -> Classifier

# Results
Best result was RoBERTEye vs the vision and other approach achieving 90 Accuracy on whether using is searching for an answer or reads for understanding
## Timing
Furthermore in 1.5 seconds we achieve 77.6% accuracy.
### Disclaimer
We made the user fixate on the first word prior to collecting data so in our expirement all users start from the first letter.
> Most paragraphs require to read mid-end parts.
# Another Expirement
Question - Whether a reader has already read a specific text
- We did notice variance in reading patterns
- Used XGBoost,
- Feature Based models outperformed the other approaches of ROBERTEye and reading speed comparison
> Question : Did you try to check few shot performance when given a specific user data prior to classification?
> Didn't fully understand if they tried it or not but seems that it should improve performance
## Another possibiliy is to check synthetic data generation

## How to leverage Eye Trackin in NLP?
We can look at human vs LLM alligment



# Code

Add link to code here (if exists)
