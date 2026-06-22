# Rap Debate TakeMeter
## Community
This project focuses on online rap and hip-hop discussion communities where fans debate artists such as Drake, Kendrick Lamar, Jay-Z, J. Cole, and others. These discussions take place on Reddit communities such as r/hiphopheads, r/rap, r/Drizzy, and r/KendrickLamar.
The quality of discussion varies significantly. Some users analyze lyrics and provide evidence-based arguments, while others post reactions, opinions, jokes, or insults. This makes rap communities a good environment for building a discourse-quality classifier.
## Research Question
Can a fine-tuned language model distinguish between different types of rap debate discourse?
## Labels
## 1. lyrical_analysis
**Definition:**
Discussion of bars, lyricism, rhyme schemes, punchlines, flow, delivery, storytelling, wordplay, or songwriting techniques.
**Examples:**
- "Jay's MSG freestyle had more lyrical density than Iceman."
- "Kendrick's repetition on Not Like Us made the record more effective."
**Uncertain Example:**
- "Family Matters was better because Drake rapped harder."
Decision Rule:
If the post discusses how the artist is rapping, classify it as `lyrical_analysis`.
-- 
## 2. evidence_based_argument

**Definition:**
Uses facts, statistics, chart performance, sales numbers, awards, influence, historical comparisons, or logical reasoning to support a claim.

**Examples:**

* "Drake has been the most streamed rapper for over a decade."
* "Jay-Z has more classic albums and a longer run at the top."

**Uncertain Example:**

* "Drake is the GOAT because he dominated charts for 15 years."

**Decision Rule:**
If the post provides evidence, statistics, achievements, influence, awards, or logical reasoning that supports the claim, classify it as `evidence_based_argument`.

 
## 3. opinion_reaction
**Definition:**
Expresses a personal opinion, belief, preference, or emotional reaction without substantial supporting evidence.
**Examples:**
- "Kendrick won."
- "I still think Drake is better."
**Uncertain Example:**
- "Jay-Z is the greatest rapper ever."
**Decision Rule:**
If the post primarily expresses a preference or conclusion without supporting evidence, classify it as opinion_reaction.
 
## 4. insult_meme
**Definition:**
Posts whose primary purpose is mockery, trolling, insults, memes, or dismissive commentary.
**Examples:**
- "Drake is a clown."
- "Trash."
**Uncertain Example:**
- "Only idiots think Drake won."
**Decision Rule:**
If ridicule or mockery is the primary purpose of the post, classify it as insult_meme.
## Edge Case

**Example:**

* "Jay-Z is better because he has more classic albums."

**Possible Labels:**

* evidence_based_argument
* opinion_reaction

**Resolution:**
If the post includes evidence, examples, statistics, influence, awards, albums, or reasoning, classify it as `evidence_based_argument`.

If the post only states a preference or ranking without supporting evidence, classify it as `opinion_reaction`.
## Difficult Annotation Cases

### Case 1

**Post:**
"Family Matters is my favorite diss track."

**Possible Labels:**

* lyrical_analysis
* opinion_reaction

**Decision:**
I labeled this as `opinion_reaction`.

**Reason:**
The comment mentions a diss track, but it does not explain anything about lyrics, flow, structure, delivery, or songwriting. It is mainly a personal preference.

---

### Case 2

**Post:**
"Drake is the GOAT because he has been the most streamed rapper for over a decade."

**Possible Labels:**

* opinion_reaction
* evidence_based_argument

**Decision:**
I labeled this as `evidence_based_argument`.

**Reason:**
The phrase "Drake is the GOAT" is an opinion, but the comment supports the claim with measurable evidence about streaming and longevity.

---

### Case 3

**Post:**
"Drake fans will not accept the L."

**Possible Labels:**

* opinion_reaction
* insult_meme

**Decision:**
I labeled this as `insult_meme`.

**Reason:**
The comment is not making a serious argument. Its main purpose is to mock Drake fans, so it fits the insult or meme category.



## Why These Labels Matter
Rap discussions frequently mix analysis, evidence-based debate, emotional reactions, and memes. These four labels capture common forms of discourse found in online rap communities while maintaining clear boundaries between categories. The goal is to determine whether a fine-tuned model can learn these distinctions and classify new posts accurately.

## Data Collection Plan

I collected examples from public Reddit communities such as r/rap, r/hiphopheads, r/Drizzy, and r/KendrickLamar. My goal was to collect at least 200 comments and label them using my four categories: lyrical_analysis, evidence_based_argument, opinion_reaction, and insult_meme.

I originally aimed for about 50 examples per label. If one category ended up with fewer examples than the others, I planned to collect more comments from that category to make the dataset more balanced.

## Evaluation Metrics

I will evaluate my classifier using accuracy, per-class accuracy, and a confusion matrix.

Accuracy shows how many predictions the model gets correct overall. Per-class accuracy helps me see how well the model performs on each label individually. The confusion matrix will help me identify which labels the model mixes up most often.

## Definition of Success

I would consider the project successful if the model achieves at least 80% overall accuracy.

I would also like each label category to have at least 70% accuracy. A useful classifier should be able to tell the difference between analysis, evidence-based arguments, opinions, and memes most of the time.

## AI Tool Plan

### Label Stress-Testing

I used ChatGPT to help test my labels by generating examples that were difficult to classify. If an example seemed to fit more than one label, I updated my definitions and decision rules to make the categories clearer.

### Annotation Assistance

I used ChatGPT to help organize and review potential examples from Reddit. However, I manually checked every example before adding it to the final dataset.

### Failure Analysis

After testing the model, I will review the examples it gets wrong. I may use ChatGPT to help identify patterns in the mistakes, but I will verify those patterns myself before including them in my final analysis.

## Baseline Results

The zero-shot Groq baseline achieved 80% accuracy on the test set.

### Per-Class Performance

| Label                   | Precision | Recall | F1-Score |
| ----------------------- | --------- | ------ | -------- |
| lyrical_analysis        | 1.00      | 0.60   | 0.75     |
| evidence_based_argument | 1.00      | 0.73   | 0.84     |
| opinion_reaction        | 0.50      | 1.00   | 0.67     |
| insult_meme             | 1.00      | 1.00   | 1.00     |

### Reflection

The baseline performed best on insult_meme, achieving perfect precision and recall. It also performed well on evidence_based_argument posts.

The model struggled most with lyrical_analysis and opinion_reaction. Lyrical analysis posts were sometimes confused with other discussion categories, while opinion_reaction was often over-predicted.

My hypothesis is that a fine-tuned model trained on rap debate discourse will better distinguish between lyrical analysis, evidence-based arguments, and opinion-based reactions than a general-purpose language model.


