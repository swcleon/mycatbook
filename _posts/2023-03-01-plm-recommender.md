---
title: Language Models as Recommender Systems-Evaluations and Limitations
categories: [all, nlp]
comments: true
usemathjax: true
---

[Zhang et al., NeurIPS 2021 Workshop ICBINB](https://openreview.net/forum?id=hFx3fY7-m9b)

## Introduction

Traditionally, there are two types of work that combine NLP and recommender systems:

1. Using textual information to augment item representations for better recommendation performance;
2. Treating items in users' interaction sequences as text tokens in natural languages.

Both types require training training models from scratch. This work converts the traditional item-based recommendation to a text-based cloze task, in the hope to tackle the zero-shot recommendations problem and the data efficiency problem. The first problem aims to generate personalized recommendations when no interation data is available fro training, while the latter wants the model to be easily adapt to a veriety of downstream tasks.

## Method

Given a user with viewed item sequence $$[x_1, x_2, \dots, x_{t-1}]$$, we want to predict the probability distribution of the next item $$p(x_t|x_1,\dots,x_{t-1})$$. In LMRecSys, we first map each item to its tokenized word description $$d(x_i) = [w_{i_1}, w_{i_2},\dots,w_{i_L}]$$ and use a prompt $$f(\cdot)$$ to convert the item sequence into the text sequence $$c = f([d(x_1), d(x_2),\dots,d(x_{t-1})])$$ as the context. We then use the language model to estimate the probability distribution of the next item by multi-token inference, which has the following challenges:

1. Different items have text descriptions of different length (use padding).
2. Wheter to estimate the probability distribution of each token in the item description independently or dependently (tradeoff between efficiency and accuracy).

## Experiments

Dataset: MovieLens-1M, which consists of 6040 users, 3883 movies and 1M interactions.

### Zero-shot Recommendations

For each user, provide the model with his/her first 5 watched movies and use the model to predicit the 6th. The movie title truncated or padded to 10 tokens length serves as the item description. The results show that:

1. Multitoken inference methods significantly influence the results show that GPT2 O(LN) shows much better performances than other influences because of the more accurate probability estimation but much more computational cost.
2. Model size and prompt have small influences on the results.
3. Language models show clear linguistic biases for recommendations and calibration slightly reduces linguistic biases.

### Finetuned Recommendations

After obtaining the item probability distribution using different multi-token inference methods, we can use the corss-entropy loss to maximize the probability of the ground-truth item. The reuslts show that:

1. LMRecSys under-performs GRU4Rec, possibly due to the intrinsically more challenging task of multi-tokens inference.
2. Domain-adaptive pretrining shows small improvements.
3. Fine-tuned LMRecSys learns how to recommend but linguistic biases still exist for bottom predictions.
