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
- 
| **Language** | **A1 & A2** | **A2 & A3** | **A3 & A1** | **Overall** |
|--------------|-------------|-------------|-------------|-------------|
| **Telugu**   | 82.50       | **87.75**   | **88.25**   | 81.00       |
| **Hindi**    | **86.45**   | **88.00**   | 79.20       | 83.15       |
| **English**  | **87.60**   | 82.00       | **89.30**   | 85.10       |
---

## Dataset Details

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
2. **Linguistic Diversity**:
   - Content was sourced from multiple platforms and languages to ensure coverage of diverse linguistic and cultural phenomena.
3. **Reducing Dataset Artifacts**:
   - Posts were carefully curated to ensure that models trained on this dataset learn meaningful patterns rather than spurious correlations.
