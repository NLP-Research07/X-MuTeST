# X-MuTeST

## Annotation Process

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

---

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
---

## Dataset Details
### Hindi and English Datasets

The Hindi and English datasets used in this research were sourced from the Hate Speech and Offensive Content Identification (HASOC) contest, which focuses on identifying hate speech and offensive language across multiple languages and dialects. 

#### Sources:
- **HASOC 2020**: Includes annotated samples from Twitter featuring instances of hate speech and offensive content.
- **HASOC 2021**: Expands on the previous year's dataset with additional annotated samples.

#### Dataset Preparation:
- Datasets from both HASOC 2020 and HASOC 2021 were combined to increase the total number of samples for both Hindi and English.
- Binary labels were applied, categorizing sentences into two classes:
  - **HATE**
  - **NOT HATE**

#### Data Splitting:
- For both Hindi and English, 15% of the combined dataset was reserved for testing to ensure reliable evaluation.

| **Metric**               | **Telugu** | **Hindi** | **English** |
|--------------------------|------------|-----------|-------------|
| **Total Records**        | 4,492      | 6,004     | 6,334       |
| **Hate Records**         | 2,131      | 2,026     | 3,767       |
| **Non-Hate Records**     | 2,361      | 3,978     | 2,567       |
| **Avg Word Count**       | 6.46       | 18.84     | 19.20       |
| **Avg Character Count**  | 68.98      | 110.93    | 100.47      |
| **Avg Rationale Length** | 3.10       | 3.26      | 3.78        |
---

## Addressing Potential Dataset Concerns

We acknowledge prior concerns about biases and artifacts in hate speech datasets. To mitigate these issues:
1. **Annotator Training**:
   - Annotators were trained to avoid biases by focusing on context and meaning, rather than personal interpretations or stereotypes.
2. **Reducing Dataset Artifacts**:
   - Posts were carefully processed and curated to ensure that models trained on this dataset learn meaningful patterns rather than spurious correlations.
