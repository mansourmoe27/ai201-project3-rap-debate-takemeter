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
Uses facts, statistics, chart performance, sales numbers, awards, influence, historical comparisons, lyrics, or logical reasoning to support a claim.
**Examples:**
- "Drake has been the most streamed rapper for over a decade."
- "Jay-Z has more classic albums and a longer run at the top."
**Uncertain Example:**
- "Drake is the GOAT because he dominated charts for 15 years."
**Decision Rule:**
If the post provides evidence or reasoning that supports the claim, classify it as evidence_based_argument.
 
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
 
### 4. insult_meme
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
- "Jay-Z is better because he has more classic albums."
**Possible Labels:**
- evidence_based_argument
- opinion_reaction
**Resolution:**
If the post includes evidence, examples, statistics, influence, awards, albums, or reasoning, classify it as evidence_based_argument.
If the post only states a preference or ranking without supporting evidence, classify it as opinion_reaction.

Why These Labels Matter
Rap discussions frequently mix analysis, evidence-based debate, emotional reactions, and memes. These four labels capture common forms of discourse found in online rap communities while maintaining clear boundaries between categories. The goal is to determine whether a fine-tuned model can learn these distinctions and classify new posts accurately.

