<img src=https://github.com/NLP-Research07/X-MuTeST/blob/main/training.png width="500" />

<img src=https://github.com/NLP-Research07/X-MuTeST/blob/main/method1.png width="500" />

# Annotation Process

## Pilot Annotation

### Objective
To identify annotators capable of understanding the nature of hate speech and effectively identifying rationales at the token level.

### Task Setup
- Annotators were provided with 15 posts and asked to:
  1. Perform hate/offensive speech classification.
  2. Highlight tokens that contributed to their decision (human rationales).
- Annotators were provided with examples of labeled posts and detailed explanations of the labeling and rationale-selection processes to ensure consistency.

### Selection Criteria
- Annotators who demonstrated high-quality annotation by accurately identifying hate speech and corresponding tokens were selected.
- Out of 10 participants in the pilot, four annotators were shortlisted for the main task such that there were three annotators for each language.
- Feedback from the pilot study was incorporated to improve instructions for the main task.
- Selected annotators are from different geolocations. They are engineering students, and in a reward, they were provided free access to our GPU servers for more than 100 hrs.


## Main Annotation Task

### Annotation Setup
- Each token was annotated by three annotators to ensure reliability.
- Annotators marked specific tokens (words or phrases) they deemed important for classifying the post as hateful, offensive, or normal.

### Conflict Resolution
- **Rationale Selection**: In cases of disagreement over token selection, tokens were included if they appeared in at least two of the three annotators’ rationale sets. This majority voting approach ensured a balanced and representative rationale selection.


### Quality Assessment
- The inter-annotator agreement scores were calculated using Cohen’s Kappa for pairwise comparisons between annotators, while the overall agreement was assessed using Fleiss' Kappa method.
  
| **Language** | **A1 & A2** | **A2 & A3** | **A3 & A1** | **Overall** |
|--------------|-------------|-------------|-------------|-------------|
| **Telugu**   | 82.50       | **87.75**   | **88.25**   | 81.00       |
| **Hindi**    | **86.45**   | **88.00**   | 79.20       | 83.15       |
| **English**  | **87.60**   | 82.00       | **89.30**   | 85.10       |


## Dataset Details
### Hindi and English Datasets

The Hindi and English datasets used in this research were sourced from the Hate Speech and Offensive Content Identification (HASOC) contest, which focuses on identifying hate speech and offensive language across multiple languages and dialects. 

#### Sources:
- **HASOC 2020**: Includes annotated samples from Twitter featuring instances of hate speech and offensive content.
- **HASOC 2021**: Expands on the previous year's dataset with additional annotated samples.

#### Dataset Preparation:
- Datasets from both HASOC 2020 and HASOC 2021 were combined to increase the total number of samples for both Hindi and English.
- Binary labels were given in the dataset, categorizing sentences into two classes:
  - **HATE**
  - **NOT HATE**

#### Data Splitting:
- For both Hindi and English, 15% of the combined dataset was reserved for testing to ensure reliable evaluation.

### Telugu Dataset
The Telugu dataset was sourced from the **Hate and Offensive Language Detection in Telugu Codemixed Text (HOLD-Telugu)** task, organized as part of **DravidianLangTech 2024**.

#### Source:
- Comments were collected from YouTube and annotated with binary class labels:
  - **HATE**
  - **NON-HATE**
- **Original Script**: The dataset was originally provided in Latin script.

#### Preprocessing:
- The text was transliterated into Telugu script using the **IndicXlit** transliteration method to ensure compatibility with language-specific models.

#### Testing Set:
- A separate testing set was included as part of the dataset for evaluation.

### Dataset Table

| **Metric**               | **Telugu** | **Hindi** | **English** |
|--------------------------|------------|-----------|-------------|
| **Total Records**        | 4,492      | 6,004     | 6,334       |
| **Hate Records**         | 2,131      | 2,026     | 3,767       |
| **Non-Hate Records**     | 2,361      | 3,978     | 2,567       |
| **Avg Word Count**       | 6.46       | 18.84     | 19.20       |
| **Avg Character Count**  | 68.98      | 110.93    | 100.47      |
| **Avg Rationale Length** | 3.10       | 3.26      | 3.78        |


## Addressing Potential Dataset Concerns

We acknowledge prior concerns about biases and artifacts in hate speech datasets. To mitigate these issues:
1. **Annotator Training**:
   - Annotators were trained to avoid biases by focusing on context and meaning, rather than personal interpretations or stereotypes.
2. **Reducing Dataset Artifacts**:
   - Posts were carefully processed and curated to ensure that models trained on this dataset learn meaningful patterns rather than spurious correlations.
---
# Methodology: Unigrams, Bigrams, and Trigrams for Contextual Analysis
X-MuTeST leverages **n-grams (unigrams, bigrams, trigrams)** to capture context up to **five words** (two to the left and two to the right of the target word). The process for computing word importance is structured as follows:

### a) Unigrams
- **Process**: Each word in the sentence is passed individually (as a unigram) to the model, and its classification probability is calculated.
- **Importance**: The importance score of the word is computed as the **difference** between:
  - The classification probability of the entire sentence.
  - The probability with just the unigram.


### b) Bigrams
- **Contextual Dependence**: Words often derive meaning from adjacent words (e.g., *"not good"* vs. *"good"*).
- **Process**:
  - All bigrams containing the target word are evaluated.
  - The classification probability for each bigram is calculated, and the **difference** from the full sentence probability is determined.
  - Since multiple bigrams exist for a word, the **average difference** is used as the score.


### c) Trigrams
- **Broader Context**: Extends the analysis to two words on either side of the target word.
- **Process**: Similar to bigrams, but considers all trigrams containing the target word.


### Aggregation of Importance Scores
- Final importance score for a word is computed by aggregating the unigram, bigram, and trigram scores using weighted contributions:
  - **Unigrams**: 0.5
  - **Bigrams**: 0.3
  - **Trigrams**: 0.2
- **Higher-Order N-Grams**: Experiments with n-grams larger than trigrams showed no improvement, as additional context did not provide meaningful information.


It is also to be noted that the proposed framework is devised to not only enhance explainability but also classification performance by incorporating 2-stage training that incorporates human-rationale in the training. Additionally, one of our major contributions lies in proposing a dataset with human-annotated datasets to address the challenges of explainable hate speech detection in under-resourced languages.

## Training Framework: Balancing Explainability and Classification

X-MuTeST achieves a balance between **explainability** and **classification performance** through a carefully designed **two-stage training framework**:


### a) Stage 1: Human Rationale Alignment
- **Objective**: Align the model's attention with **human-provided rationales** to improve explainability.
- **Process**:
  - The encoder is trained for a few epochs (three in this case).
  - Human rationales are used as the **target attention mask** during this stage.
- **Outcome**: This stage ensures the model learns to focus on tokens deemed important by humans, enhancing interpretability.


### b) Stage 2: Explainability-Driven Training
- **Objective**: Incorporate **model-driven insights** alongside human rationales to enhance performance.
- **Process**:
  - Training continues using **attention masks** generated by the proposed X-MuTeST method.
  - These masks include:
    - Tokens identified by human rationales.
    - Tokens deemed important by the encoder based on contextual dependencies.
- **Outcome**: The model learns to balance **human understanding** and **model-driven insights**, ensuring both explainability and classification performance.


### Benefits of the Two-Stage Process
1. **Stage 1**:
   - Aligns the encoder with human rationales.
   - Prevents over-reliance on model-driven insights during early training.
2. **Stage 2**:
   - Refines the model by focusing on tokens that contribute to sequence classification.
   - Maintains a balance between explainability and predictive accuracy.

This dual-stage approach enables X-MuTeST to achieve **improved explainability** and **classification performance** simultaneously.


# Advantages of X-MuTeST over Other Methods

Our explainability method, **X-MuTeST**, introduces several distinct advantages compared to existing approaches, especially in the domain of hate speech detection:


## a) Comparison with Attention-Based Methods
- **Limitations of Attention-Based Methods**:
  - Attention weights are often entangled with model predictions, which can make them unreliable indicators of token importance.
  - There is ongoing debate about whether attention weights should be considered valid explainability scores.
    - **Against Attention**: Jain and Wallace [1].
    - **In Favor of Attention**: Wiegreffe and Pinter [2].
- **X-MuTeST Advantage**:
  - Unlike attention-based methods, X-MuTeST directly computes token importance from model outputs using **contextual perturbations**, offering a more interpretable and grounded explanation mechanism.


## b) Comparison with Integrated Gradients (IG)
- **Limitations of IG**:
  - IG attributes feature importance using gradients from a baseline to the actual input but may overlook the contextual influence of neighboring words.
- **X-MuTeST Advantage**:
  - Explicitly evaluates **contextual dependencies** using **bigrams and trigrams**.
  - This is particularly valuable for hate speech detection, where context often changes the semantic meaning of words.


## c) Enhanced Context Capturing Through Multi-Gram Analysis
- **Comparison with N-Gram Approaches**:
  - Prior n-gram-based methods, such as Kohli and Devi [3], use only trigrams for generating explanations.
- **X-MuTeST Advantage**:
  - Extends context analysis to **unigrams, bigrams, and trigrams**, capturing word dependencies up to five words (two on each side of the target word).
  - Final importance scores are aggregated using weighted contributions:
    - **Unigrams**: 0.5
    - **Bigrams**: 0.3
    - **Trigrams**: 0.2
  - This hierarchical approach enhances the interpretability of hate speech explanations, accounting for the nuanced influence of surrounding context.


## d) Comparison with LIME
- **Limitations of LIME**:
  - Generates explanations by sampling sentence formations based on a fixed feature count.
  - Challenges with feature count selection:
    - **Low feature count**: Misses important contextual word combinations.
    - **High feature count**: Includes redundant or less meaningful combinations, increasing computational cost without adding value.
- **X-MuTeST Advantage**:
  - Systematically evaluates all possible **n-grams** (up to trigrams) for every word in a sentence.
  - Ensures comprehensive context analysis without unnecessary computational overhead.
  - Experiments (Tables 3, 4, and 5) show that X-MuTeST outperforms LIME (denoted as **L**) and HateXplain (denoted as **RL**) in providing reliable explanations.


1. **Jain, S., & Wallace, B. C. (2019)**. Attention is not Explanation. In *Proceedings of NAACL-HLT 2019* (pp. 3543–3556).
2. **Wiegreffe, S., & Pinter, Y. (2019)**. Attention is not not explanation. In *Proceedings of EMNLP-IJCNLP 2019*.
3. **Kohli, A., & Devi, V. S. (2023)**. Explainable offensive language classifier. In *International Conference on Neural Information Processing* (pp. 299–313).
4. **Ribeiro, M. T., Singh, S., & Guestrin, C. (2016)**. "Why should I trust you?" Explaining the predictions of any classifier. In *Proceedings of the 22nd ACM SIGKDD* (pp. 1135–1144).
5. **Mathew, B., Saha, P., Yimam, S. M., Biemann, C., Goyal, P., & Mukherjee, A. (2021)**. HateXplain: A benchmark dataset for explainable hate speech detection. In *Proceedings of AAAI 2021* (Vol. 35, No. 17, pp. 14867–14875).
