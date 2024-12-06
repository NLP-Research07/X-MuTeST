# X-MuTeST

## Abstract

Hate speech detection on social media presents ongoing challenges, particularly in proposing methods that are not only accurate but also explainable. Since Indic languages are underexplored in this domain, we extend this research to include explainability in hate speech detection for under-resourced languages such as Hindi and Telugu alongside English. To this end, we provide human-annotated rationales for each word of the post to identify text segments that justify the assigned class label. We also propose an e**X**plainable **M**ultilingual ha**T**e **S**peech de**T**ection, **X-MuTeST**, method for Indic languages. X-MuTeST explainability method is based on the difference between the prediction probabilities of the original text and those of unigrams, bigrams, and trigrams.

We first demonstrate that leveraging human rationales during training improves both the classification performance and the model’s ability to justify its decisions. Additionally, we demonstrate through experiments that injecting human rationales with the proposed explainability method to enhance the \textit{attention} of the model during the training further improves its classification as well as explainability performance. For explainability, we use Plausibility metrics such as Token-F1 and IOU-F1, as well as Faithfulness metrics such as Comprehensiveness and Sufficiency. For sequence classification, we utilize standard metrics such as accuracy, F1, and macro-F1. By focusing on explainability for under-resourced languages, we aim to advance hate speech detection across diverse linguistic contexts. We have annotated 6,004, 4,492, and 6,334 samples for token-level rationales for Hindi, Telugu, and English, respectively. Our annotated datasets and code will be publicly available on GitHub.

## Annotation Process:
###Pilot Annotation:

Objective: To identify annotators capable of understanding the nuanced nature of hate speech and effectively identifying rationales at the token level.
Task Setup: Annotators were provided with 20 posts and asked to:
a) Perform hate/offensive speech classification.
b) Highlight tokens that contributed to their decision (human rationales).
Training Material: Annotators were provided with examples of labeled posts and detailed explanations of the labeling and rationale-selection processes to ensure consistency.
Selection Criteria: Annotators who demonstrated high-quality annotation by accurately identifying hate speech and corresponding tokens were selected. Out of 621 participants in the pilot, 253 annotators were shortlisted for the main task. Feedback from the pilot study was incorporated to improve instructions for the main task.
