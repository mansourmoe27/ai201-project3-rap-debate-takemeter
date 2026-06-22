# ai201-project3-rap-debate-takemeter
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

## Labels

### lyrical_analysis

Discussion of bars, lyricism, rhyme schemes, punchlines, flow, delivery, storytelling, wordplay, or songwriting techniques.

Example:

> "Jay's MSG freestyle had more lyrical density than Iceman."

### evidence_based_argument

Uses facts, statistics, chart performance, sales numbers, awards, influence, historical comparisons, or logical reasoning to support a claim.

Example:

> "Drake has been the most streamed rapper for over a decade."

### opinion_reaction

Expresses a personal opinion, preference, belief, ranking, or emotional reaction without substantial supporting evidence.

Example:

> "Kendrick won."

### insult_meme

Posts whose primary purpose is mockery, trolling, insults, memes, or dismissive commentary.

Example:

> "Drake is a clown."

---

## Dataset

* Total examples: 231
* Labels: 4
* Train set: 161 examples
* Validation set: 35 examples
* Test set: 35 examples

Dataset file:

`rap_debate_dataset.csv`

---

## Baseline Results (Groq)

The zero-shot baseline used Groq's Llama 3.3 70B model with prompt-based classification.

### Accuracy

77.1%

---

## Fine-Tuned DistilBERT Results

A DistilBERT classifier was fine-tuned for 3 epochs using the labeled dataset.

### Accuracy

48.6%

---

## Results Comparison

| Model                   | Accuracy |
| ----------------------- | -------- |
| Groq Zero-Shot Baseline | 77.1%    |
| Fine-Tuned DistilBERT   | 48.6%    |

Fine-tuning resulted in a performance decrease of 28.6 percentage points compared to the baseline.

---

## Error Analysis

The fine-tuned model performed best on evidence_based_argument examples but struggled with opinion_reaction and insult_meme examples.

One possible explanation is that the dataset was relatively small for training a transformer model. Many rap discussion posts contain overlapping characteristics such as opinions, evidence, humor, and analysis, making classification difficult.

The Groq baseline likely benefited from broader language understanding and world knowledge, while the fine-tuned DistilBERT model relied entirely on the limited labeled dataset.

---

## Files

* planning.md
* rap_debate_dataset.csv
* evaluation_results.json
* confusion_matrix.png

---

## AI Usage

ChatGPT was used for label stress-testing, dataset organization, annotation review, and failure analysis. All labels were manually reviewed before inclusion in the final dataset.
