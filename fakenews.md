---
layout: page
title: "Fake News Detection"
permalink: /fakenewsllm
---

# Fake News Detections Using LLMs


## Overview

The goal of this research is to explore the use of Large Language Models (LLMs) to enhance the ability of smaller language models to detect of fake news. The primary dataset under consideration is the LIAR dataset, which offers metadata on each claim, facilitating the training of models on specific domains such as healthcare and politics.

## Methodology

### Initial Concept

The original idea is to use LLMs to reason over supporting documents and determine what information is needed to determine if a claim is true. For example, if one saw a claim online saying "The Pope was born in 1844!", one would verify this by looking up the Pope's age, and seeing that he's 87. I'm modeling my idea on this thought process.  The process involves:

1. **Identifying Relevant Documents:** Articles are sourced from the internet.
2. **Generating Search Queries:** An LLM (e.g., GPT-3.5 or GPT-4) is employed to formulate search queries aimed at finding evidence supporting or refuting the claim.

    **Example:**
    - **Claim:** "We have fewer Americans working now than in the 70s."
    - **Search Query:** "American employment rate compared to the 70s"

### Constraining Sources

Given the vastness of the internet, the search results are constrained to a set of unbiased news sites recommended by Allsides.com, including BBC, Reuters, APNews, and The Hill.

**Example:**
- **Claim:** "We have fewer Americans working now than in the 70s."
- **Search Query:** "American employment rate compared to the 70s The Hill"

### Extracting Relevant Text

After parsing the HTML of the articles, the supporting or opposing text might only constitute a sentence or two. To avoid exceeding the maximum token limits of LLMs and to improve efficiency, a 4 span of text with the closest cosine similarity to the claim is extracted. This extracted text is then fed into a smaller language model for classification.

### Prediction

Finally, the evidence and claim are fed to a smaller language model for prediction.

### Current Challenges

There are many things I'm working to refine in this process, including the use of knowledge distilled models from proprietary LLMs, alternate text extraction metrics, and ways of escaping API rate limits.

The LIAR dataset has about 12,000 examples across the train, test, and validation splits. Doing a search for all of these would cost me $300 using the Bing API. I was able to use the free tier to find internet evidence for the validation set, but that's it so far.
  

---


