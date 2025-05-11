# TLDR: EVALTREE Paper & Our Research
The paper introduces EVALTREE, a method to find exactly why an AI model fails by building a "skill tree" of a benchmark (like a map of all the skills tested). It uses AI to label each question with a skill, turns skills into numerical codes, clusters them to build a hierarchy (tree), and labels the tree branches. Then, it checks performance at every point in the tree and uses statistics to find skills where the model is significantly weak, giving us a "weakness profile".
How it helps us:
 * Structure Weakness: Our method finds weak questions via variations. We can potentially map these onto an EVALTREE-like skill tree to see what underlying skills those questions/variations relate to.
 * Targeted Data: The paper shows generating data based on identified weak skills (like those from the tree) is super effective for improving models. We can use this idea to guide our dataset generation, focusing on the specific skills where our variation analysis shows the model struggles.
 Okay, let's go through the entire EVALTREE process in detail, sticking to the understanding that helped you, like building and using a skill map.
Part 1: Building the Skill Map (Capability Tree Construction)
This part creates a detailed, hierarchical map of all the different skills covered by a benchmark (like a big test for an AI model). It has four steps:
 * Skill Labeling for Each Question (Capability Annotation):
   * Purpose: To understand exactly what specific skill each individual question in the benchmark is testing.
   * Process: EVALTREE uses another Language Model (LM) to analyze each question and its correct answer. It asks the LM to provide a short phrase describing the specific skill or capability needed to solve that particular problem. The goal is to get a detailed, action-oriented description without mentioning the specific content of the question.
   * Outcome: Every single question in the benchmark gets a natural language label describing the skill it tests. These individual questions/instances will become the "leaves" of our skill tree.
 * Turning Skill Labels into Digital Codes (Capability Embedding):
   * Purpose: To convert the natural language skill descriptions into a numerical format that computers can easily process and group based on similarity.
   * Process: EVALTREE uses a sentence embedding model (a type of AI model that turns text into numerical vectors) to convert the skill description from Step 1 for each instance into a vector (a list of numbers). Skills that are semantically similar (mean similar things) will have numerical vectors that are close to each other in this multi-dimensional space.
   * Outcome: Each question instance, now labeled with a skill, is associated with a numerical vector representing that skill.
 * Organizing Skills into a Hierarchy (Recursive Clustering-Based Construction):
   * Purpose: To build the tree structure, grouping similar skills together into broader and broader categories as you move up the hierarchy.
   * Process: EVALTREE starts with all the numerical skill vectors from Step 2 at the "root" (the very top, representing all skills). It then uses a clustering algorithm (specifically K-Means) to group these vectors into a few initial clusters based on their numerical similarity. It tries different numbers of clusters and uses a measure called the Silhouette score to figure out which number of clusters creates the best, most distinct groups. Each of these clusters becomes a "child" node (a branch) of the current node, and the instances whose skill vectors are in that cluster are linked to that child node. This process is then repeated recursively for each new child node – the skill vectors linked to that node are clustered again to create finer-grained sub-categories. This continues until nodes only have a small number of instances, forming the leaves of the tree.
   * Outcome: A hierarchical tree structure is formed. The top nodes represent broad skill categories, and the nodes branch down to more specific skills, with individual questions (instances) as the leaves.
 * Labeling the Skill Groups (Capability Description):
   * Purpose: To give human-understandable natural language descriptions to the skill categories represented by each node (group of instances) in the tree created in Step 3.
   * Process: For the leaf nodes (individual instances), their description is simply the skill label from Step 1. For all the non-leaf nodes (the branches and the trunk), EVALTREE uses an LM again. It gives the LM the skill descriptions of the child nodes (the smaller groups below it) and asks the LM to summarize them into a single, overarching natural language description for that node.
   * Outcome: Every node in the capability tree, from the broad root to the specific branches just above the leaves, has a natural language label describing the skill category it represents.
At the end of Part 1, you have the completed Capability Tree – a detailed, multi-level map of skills with every benchmark question located as a leaf and every grouping of questions labeled with a skill description.
Part 2: Using the Skill Map to Find Weak Spots (Generating a Weakness Profile)
This part uses the skill map and the AI model's performance on the test questions to pinpoint exactly where the model is struggling.
 * Calculate Performance at Every Skill Level:
   * Process: EVALTREE takes the known performance of the AI model on each individual test question (the leaves of the tree). For every node in the tree (every skill category, from the most specific to the most general), it calculates the model's performance based on the performance of all the instances linked to that node. If it's accuracy, it calculates the percentage of correctly answered questions under that node. If it's win-rate, it calculates the win-rate on those questions.
   * Outcome: Every node in the capability tree now has an associated performance metric for the AI model.
 * Statistically Testing for Low Performance:
   * Purpose: To determine if the performance at a node is not just a bit low, but statistically significantly lower than a certain level, meaning the model is genuinely struggling with that skill.
   * Process: You set a threshold performance level \tau that you care about (e.g., if you want to find skills where the model performs below 60% accuracy, \tau = 60\%). EVALTREE performs a binomial test for each node. This test looks at the number of instances under that node and how many the model got right (or won). It calculates the probability of getting that result if the model's true skill level was \tau or higher. If this probability is very low (below a significance level \alpha, usually 0.05), it means the performance is statistically significantly lower than \tau.
   * Outcome: For each node, EVALTREE knows if the model's performance is statistically significantly low compared to the threshold \tau.
 * Extracting the Weakness Nodes:
   * Purpose: To select the specific nodes in the tree that represent the model's weaknesses at an appropriate level of detail.
   * Process: EVALTREE traverses the tree again. A node is identified as a weakness and extracted for the weakness profile if two main conditions are met:
     * The node itself shows statistically significantly low performance (based on the test in step 2).
     * Its direct child nodes (representing more specific sub-skills) that have enough instances also show statistically significantly low performance. This prevents labeling a broad skill as a weakness if the problem is actually concentrated in just one or two very specific sub-skills under that category.
   * The traversal stops going down a branch if the nodes have too few instances or if a node has already been extracted (to avoid redundant weaknesses).
   * Outcome: A final list of nodes is extracted. The weakness profile consists of the natural language capability descriptions of these extracted nodes.
So, after building the detailed skill map (Part 1), EVALTREE uses the model's performance and statistical tests on that map (Part 2) to navigate the hierarchy and identify the specific skill areas where the model reliably underperforms, providing an interpretable list of its weaknesses.

