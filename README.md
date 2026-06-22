# Rap Debate TakeMeter

## Project Overview

Rap Debate TakeMeter is a text classification project that analyzes online rap and hip-hop discussions. The goal is to classify comments into different types of discourse commonly found in rap communities.

This project was completed as part of AI201 Project 3 and follows the complete machine learning workflow of dataset collection, annotation, fine-tuning, evaluation, and comparison against a baseline model.

---

## Community

The dataset was collected from public online rap discussion communities including:

* r/rap
* r/hiphopheads
* r/Drizzy
* r/KendrickLamar

These communities contain a mix of lyric analysis, debate, opinions, memes, and arguments, making them a good environment for a discourse classification task.

---

## Label Taxonomy

### 1. lyrical_analysis

Discussion of bars, lyricism, rhyme schemes, punchlines, flow, delivery, storytelling, wordplay, or songwriting techniques.

Examples:

> "Jay's MSG freestyle had more lyrical density than Iceman."

> "Kendrick's repetition on Not Like Us made the record more effective."

---

### 2. evidence_based_argument

Uses facts, statistics, chart performance, sales numbers, awards, influence, historical comparisons, or logical reasoning to support a claim.

Examples:

> "Drake has been the most streamed rapper for over a decade."

> "Jay-Z has more classic albums and a longer run at the top."

---

### 3. opinion_reaction

Expresses a personal opinion, preference, belief, ranking, or emotional reaction without substantial supporting evidence.

Examples:

> "Kendrick won."

> "I still think Drake is better."

---

### 4. insult_meme

Posts whose primary purpose is mockery, trolling, insults, memes, or dismissive commentary.

Examples:

> "Drake is a clown."

> "Trash."

---

## Dataset

* Total examples: 231
* Labels: 4
* Train set: 161 examples
* Validation set: 35 examples
* Test set: 35 examples

Dataset file:

`rap_debate_dataset.csv`

### Label Distribution

Include the actual counts from your dataset here.

| Label                   | Count |
| ----------------------- | ----: |
| lyrical_analysis        |    XX |
| evidence_based_argument |    XX |
| opinion_reaction        |    XX |
| insult_meme             |    XX |

---

## Data Collection Process

Examples were manually collected from public Reddit rap communities. Each post was reviewed individually and assigned one label based on the definitions established in planning.md.

The goal was to maintain a balanced dataset across all four categories and avoid a situation where one category dominated the training set.

---

## Difficult Annotation Cases

### Case 1

Post:

> "Family Matters is my favorite diss track."

Possible Labels:

* lyrical_analysis
* opinion_reaction

Decision:

I labeled this as opinion_reaction because the comment expresses a preference without discussing lyrics, flow, delivery, or songwriting.

---

### Case 2

Post:

> "Drake is the GOAT because he has been the most streamed rapper for over a decade."

Possible Labels:

* opinion_reaction
* evidence_based_argument

Decision:

I labeled this as evidence_based_argument because the claim is supported with measurable evidence.

---

### Case 3

Post:

> "Drake fans will not accept the L."

Possible Labels:

* opinion_reaction
* insult_meme

Decision:

I labeled this as insult_meme because the primary purpose of the comment is mockery rather than discussion.

---

## Fine-Tuning Approach

Base Model:

`distilbert-base-uncased`

Training Configuration:

* Epochs: 3
* Learning Rate: 2e-5
* Batch Size: 16

I used the default notebook settings because they are commonly used for text classification tasks and were appropriate for the size of my dataset.

---

## Baseline Model

The baseline model used Groq's `llama-3.3-70b-versatile` model.

The prompt included definitions for all four labels and instructed the model to return only the label name for each post.

The baseline was evaluated on the same test set used for the fine-tuned model.

---

## Evaluation Results

### Accuracy Comparison

| Model                   | Accuracy |
| ----------------------- | -------: |
| Groq Zero-Shot Baseline |    77.1% |
| Fine-Tuned DistilBERT   |    48.6% |

The fine-tuned model performed 28.6 percentage points worse than the zero-shot baseline.

---

## Fine-Tuned Model Metrics

| Label                   | Precision | Recall |   F1 |
| ----------------------- | --------: | -----: | ---: |
| lyrical_analysis        |      0.33 |   0.60 | 0.43 |
| evidence_based_argument |      0.65 |   1.00 | 0.79 |
| opinion_reaction        |      0.00 |   0.00 | 0.00 |
| insult_meme             |      0.00 |   0.00 | 0.00 |

---

## Confusion Matrix

See `confusion_matrix.png` for the full visualization.

The confusion matrix shows that the model frequently confused opinion-based and meme-based comments with evidence-based arguments and lyrical analysis.

---

## Failure Analysis

### Example 1

True Label:

`opinion_reaction`

Predicted Label:

`evidence_based_argument`

Analysis:

The model appeared to focus on artist comparison language rather than the lack of supporting evidence.

---

### Example 2

True Label:

`insult_meme`

Predicted Label:

`opinion_reaction`

Analysis:

Short meme-like comments often lack enough context for the model to distinguish mockery from ordinary opinions.

---

### Example 3

True Label:

`lyrical_analysis`

Predicted Label:

`evidence_based_argument`

Analysis:

Posts discussing lyric quality sometimes resemble arguments because they include comparisons and reasoning.

---

## Sample Classifications

| Example                                                      | Predicted Label         |
| ------------------------------------------------------------ | ----------------------- |
| "Drake is a clown."                                          | insult_meme             |
| "Kendrick won."                                              | opinion_reaction        |
| "Jay had better wordplay on the freestyle."                  | lyrical_analysis        |
| "Drake has been the most streamed rapper for over a decade." | evidence_based_argument |

One correctly classified example was:

> "Jay had better wordplay on the freestyle."

This prediction is reasonable because the comment directly discusses lyrical technique.

---

## Reflection

My goal was to teach the model to distinguish between analysis, evidence-based arguments, opinions, and memes.

The model learned some of these distinctions, particularly evidence-based arguments, but struggled with opinion_reaction and insult_meme categories. This suggests that the model relied heavily on keywords and surface-level patterns rather than fully understanding discourse intent.

The Groq baseline benefited from broader language understanding and significantly outperformed the fine-tuned DistilBERT model.

---

## Spec Reflection

The project specification helped me think carefully about label definitions before collecting data. Establishing clear decision rules early made annotation more consistent.

One way my implementation differed from my expectations was that the fine-tuned model did not outperform the baseline. I originally expected task-specific training to improve performance, but the baseline performed substantially better.

---

## Files

* planning.md
* rap_debate_dataset.csv
* evaluation_results.json
* confusion_matrix.png
* ai201_project3_takemeter.ipynb

---

## AI Usage

1. I used ChatGPT to stress-test my label definitions by generating examples that sat between two labels.

2. I used ChatGPT to help organize and review difficult annotation decisions before adding examples to the dataset.

3. I used ChatGPT during failure analysis to identify patterns among incorrect predictions and suggest possible explanations.

All final labeling decisions were reviewed manually before inclusion in the dataset.
