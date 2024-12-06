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
- Out of 10 participants in the pilot, three annotators were shortlisted for the main task.
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

---

## Dataset Details

- **Total Posts**: 20,148
  - 9,055 posts from Twitter
  - 11,093 posts from Gab
- **Annotations**:
  - Each post is accompanied by token-level rationales highlighting important words or phrases for classification.
- **Sampling Strategy**:
  - Posts were sampled from existing hate speech datasets and manually filtered to ensure diversity in content and linguistic complexity, particularly for under-resourced languages like **Hindi** and **Telugu**.

---

## Addressing Potential Dataset Concerns

We acknowledge prior concerns about biases and artifacts in hate speech datasets. To mitigate these issues:
1. **Annotator Training**:
   - Annotators were trained to avoid biases by focusing on context and meaning, rather than personal interpretations or stereotypes.
2. **Linguistic Diversity**:
   - Content was sourced from multiple platforms and languages to ensure coverage of diverse linguistic and cultural phenomena.
3. **Reducing Dataset Artifacts**:
   - Posts were carefully curated to ensure that models trained on this dataset learn meaningful patterns rather than spurious correlations.
