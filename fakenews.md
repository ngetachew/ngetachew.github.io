---
layout: page
title: "Fake News Detection"
permalink: /URL-PATH
---

# Fake News Detections Using LLMs

I'm tyring to figure out ways of using LLMs and the internet for fake news detection. Below I will document my progress

### Initial 

Using the LIAR dataset, I tried to input potentially fake claims into ChatGPT and asked it to come up with a search query that would help figure out if it was fake or not. The plan was to actually search the internet(through Google) for answers to these questions. Unfortunately, since there are 12,000 examples in the LIAR dataset, I was unable to do this for all the examples, in fact I was only able to do it for a small portion of them. However, feeding these question responses to an untrained BERT model increased its zero shot accuracy by a noticable amount. Doing this with an already fine-tuned BERT model, however, decreases its accuracy.

Web scraping the search results presented a significant challenge as well, since the websites that the search results came up with varied a lot. I ended up having to implement a retry loop, where if my web scraping code failed on one website, it would iterate through the top results until it was able to parse something. Even then, I would dump the whole body into the input of BERT. There were a few examples that exceeded the max input size for the models, so I used GPT to summarize the inputs on this small set. Overall, this piepline is not sustainable.

After tinkering aroud with the data some more, I'm going to explore using a pre-defined set of articles/ web pages in order to constrain this problem a bit. I'll look at statements from the LIAR dataset that are based on the subject of healthcare, and define some websites/news sources that I can easily scrape from. With these sources defined, I will let GPT decided which source to pull from, then query it, and then use the results in order to support classification.


### 5/28

I'm looking into more papers where authors connect language models to knowledge bases or the internet. I found an article that scrapes the web using Bing API and finds relevant words to each potentiall fake claim using word similarity. I haven't been able to find the techniques they use to actually clean the web results. Part of me thinks that if I just obtained an LLM representation of a webpage by passing it into an LLM like BERT, then the attention weights for the HTML text would likely be similar across all articles, and a model would be able to learn this and not pay attention to it. That way, I wouldn't have to do any preprocessing at all.

