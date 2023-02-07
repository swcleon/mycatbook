---
title: Text Data augmentation for Deep Learning
categories: [all, nlp]
comments: true
---

[shorten et al. Journal of Big Data (2021)8:101.](https://doi.org/10.1186/s40537-021-00492-0)

## Text Data Augmentations

Strategies to prevent overfitting via regularization.

### Symbolic

Great interpretability for human designers. Works better with short transformations, such as replacing words or phrases, but limited in applying global transformations such as augmenting entire sentences or paragraphs.

#### Rule-based

| Easy Data Augmentation (EDA) | Example |
| --- | --- |
| **Random Swap** | I am jogging -> I tiger jogging |
| **Random Insertion** | I am jogging -> I am salad jogging |
| **Random Deletion** | I am jogging -> I jogging |
| **Random Synonym Replacement** | I am jogging -> I am running |

EDA is relatively easy to use off-the-shelf. Particularly, **Random Swap** is good for introducing semantic invariances, e.g., "I am jogging" is much more similar to "I am swimming" than "I am yelling".

Another rule-based strategy is **Regex Augmentation**, one of the most common way to clean data that has been scraped from the internet. It can also be used to find common forms of language and generate extensions that align with a graph-structured grammar, e.g., matching patterns like "This object is adj." and extending it with "and adj.", or reordering it to "A(n) adj. object".

Some other strategies like **Inversion** and **Passivization** rely on syntactic heuristics.

#### Graph-structured

> A topological space is a more general mathematical space with less constraints than Euclidean or metric spaces.

This category includes relation and entity encodings in a knowledge graph, grammatical structures in a syntax tree, or metadata grounding language data (e.g. citation networks). The addition of structure can aid in finding label-preserving transformations, representation analysis, and adding prior knowledge to the dataset.

A Knowledge graph with "is equivalent" relationships is suitale for implementing synonym swap. One example is WordNet, which describes a graph where each node is related to another graph by being a "synset".

The augmentation of these auxilliary graphs may be benefitial as well.

#### MixUp

This strategy describes forming new examples by meshing existing examples together, sometimes blending the labels as well. It varies by how the samples are interpolated, that is, at what levels of granularity (word, sentence, etc.).

#### Feature space

This strategy describes augmenting data in the intermediate representation space of Deep Neural Networks. It isolates intermediate features and apply noise (e.g. standard, gaussian, etc.) to form new data instances. Some popular implementations of feature space augmentation are presented in the figure below:

![Directions for feature space augmentation explored in MODALS](..\assets\img\feat_aug_modals.jpg)

- **Hard example interpolation (a)** forms a new example by moving it in the direction of existing embeddings that lie on the decision boundary for classifcation.
- **Hard example extrapolation (b)** describes moving existing examples along the same angle they currently lie from the mean vector of the class boundary.
- **Gaussian noise (c)** entails adding Gaussian noise in the feature space.
- **Diference transform (d)** moves an existing sample in the directional distance calculated from two separate points in the same class.

Feature space augmentations also include **Differentiable Data Augmentation**, which acts as a module that let gradient signals pass through itself.

### Neural

### Label
