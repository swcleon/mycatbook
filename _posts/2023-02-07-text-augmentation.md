---
title: Text Data augmentation for Deep Learning
categories: [all, nlp]
comments: true
---

[shorten et al. Journal of Big Data (2021)8:101.](https://doi.org/10.1186/s40537-021-00492-0)

## 1. Symbolic

Great interpretability for human designers. Works better with short transformations, such as replacing words or phrases, but limited in applying global transformations such as augmenting entire sentences or paragraphs.

### 1.1 Rule-based

![Easy Data Augmentations](..\assets\img\easy_data_augmentation.jpg)

EDA is relatively easy to use off-the-shelf. Particularly, **Random Swap** is good for introducing semantic invariances, e.g., "I am jogging" is much more similar to "I am swimming" than "I am yelling".

Another rule-based strategy is **Regex Augmentation**, one of the most common way to clean data that has been scraped from the internet. It can also be used to find common forms of language and generate extensions that align with a graph-structured grammar, e.g., matching patterns like "This object is adj." and extending it with "and adj.", or reordering it to "A(n) adj. object".

Some other strategies like **Inversion** and **Passivization** rely on syntactic heuristics.

### 1.2 Graph-structured

> A topological space is a more general mathematical space with less constraints than Euclidean or metric spaces.

This category includes relation and entity encodings in a knowledge graph, grammatical structures in a syntax tree, or metadata grounding language data (e.g. citation networks). The addition of structure can aid in finding label-preserving transformations, representation analysis, and adding prior knowledge to the dataset.

A Knowledge graph with "is equivalent" relationships is suitale for implementing synonym swap. One example is WordNet, which describes a graph where each node is related to another graph by being a "synset".

The augmentation of these auxilliary graphs may be benefitial as well.

### 1.3 MixUp

This strategy describes forming new examples by meshing existing examples together, sometimes blending the labels as well. It varies by how the samples are interpolated, that is, at what levels of granularity (word, sentence, etc.).

### 1.4 Feature space

This strategy describes augmenting data in the intermediate representation space of Deep Neural Networks. It isolates intermediate features and apply noise (e.g. standard, gaussian, etc.) to form new data instances. Some popular implementations of feature space augmentation are presented in the figure below:

![Directions for feature space augmentation explored in MODALS](..\assets\img\feat_aug_modals.jpg)

- **Hard example interpolation (a)** forms a new example by moving it in the direction of existing embeddings that lie on the decision boundary for classifcation.
- **Hard example extrapolation (b)** describes moving existing examples along the same angle they currently lie from the mean vector of the class boundary.
- **Gaussian noise (c)** entails adding Gaussian noise in the feature space.
- **Diference transform (d)** moves an existing sample in the directional distance calculated from two separate points in the same class.

Feature space augmentations also include **Differentiable Data Augmentation**, which acts as a module that let gradient signals pass through itself.

## 2. Neural

The following augmentations rely on auxiliary neural networks to generate new training data.

### 2.1. Back-translation

This strategy describes translating text from one language to another and then back from the translation to the original language. It leverages the semantic invariances encoded in supervised translation datasets to produce semantic invariances for the sake of augmentation. In machine translation, this is a convenient way to obtain a sizable parallel corpus.

### 2.2. Style

This strategy describes transferring the writing style of one author to another for applications such as abstractive summarization or context for extractive question answering, which offers an interesting window to extract semantic similarities between writing styles.

### 2.3. Generative

### 3. Label
