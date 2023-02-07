---
title: Text Data augmentation for Deep Learning
categories: [all, nlp]
comments: true
---

[shorten et al. Journal of Big Data (2021)8:101.](https://doi.org/10.1186/s40537-021-00492-0)

## 1. Symbolic Augmentations

Great interpretability for human designers. Works better with short transformations, such as replacing words or phrases, but limited in applying global transformations such as augmenting entire sentences or paragraphs.

### 1.1 Rule-based

![Easy Data Augmentations](..\assets\img\easy_data_augmentation.jpg)

EDA is relatively easy to use off-the-shelf. Particularly, Random Swap is good for introducing semantic invariances, e.g., "I am jogging" is much more similar to "I am swimming" than "I am yelling".

Another rule-based strategy is Regex Augmentation, one of the most common way to clean data that has been scraped from the internet. It can also be used to find common forms of language and generate extensions that align with a graph-structured grammar, e.g., matching patterns like "This object is adj." and extending it with "and adj.", or reordering it to "A(n) adj. object".

Some other strategies like Inversion and Passivization rely on syntactic heuristics.

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

## 2. Neural Augmentations

The following augmentations rely on auxiliary neural networks to generate new training data.

### 2.1. Back-translation

This strategy describes translating text from one language to another and then back from the translation to the original language. It leverages the semantic invariances encoded in supervised translation datasets to produce semantic invariances for the sake of augmentation. In machine translation, this is a convenient way to obtain a sizable parallel corpus.

### 2.2. Style

This strategy describes transferring the writing style of one author to another for applications such as abstractive summarization or context for extractive question answering, which offers an interesting window to extract semantic similarities between writing styles.

### 2.3. Generative

Taking an embedding of the class label as input, C-BERT augments data by replacing masked out tokens of the original instance.

Prompting repurpose the interface of masking out tokens, where the output of language models can be guided with text templates for the sake of generating or labeling new data. It has a few popular implementational variants, including in-context learning, pattern-exploiting, and prompt tuning.

In-context learning is best known for its application on the famous GPT-3. It prepends each input with a fixed task description and a collection of examples of the task. Experiments show that scale is crucial to making this work.

Prompt Tuning first embeds the prompt into a continuous space and then optimize the embedding with gradient descent while keeping the rest of the network frozen. This technique is more in line with research on Transfer Learning with minimal modifications.

Pattern exploiting training (PET) uses the pre-trained language model to label task-specific unlabeled data. This is done with manually-defined templates that convert the supervised learning task into a language modeling task. The outputs of the language model are then mapped to supervised learning labels with a verbalizer.

## 3. Label Augmentations

The most successful example of this category is Knowledge Distillation, which transforms the traditional one-hot encoded $y$ labels into a soft distribution by relabeling $x$ with the logits of another neural network's prediction. Several other strategies have been developed to augment the label space, such as label smoothing and meta-controller.

## 4. Practical Considerations for Implementation

Some details of implementing Text Data Augmentation that make a large performance difference in terms of evaluation metrics and training efficiency.

### 4.1. Consistency Regularization

A consistency loss requires a model to minimize the distance in representations of an instance and the augmented example derived from it. This is usually implemented in a multi-task learning framework where a model simultaneously optimizes the down stream task and a secondary consistency term.

### 4.2. Contrastive Learning

This strategy utilize negative samples to normalize the loss function. It makes the representation of an instance and a transformation-derived pair similar, while adding a negative normalization that pushes these representations away from other instances in the samples mini-batch.

### 4.3. Augmentation Controllers

Controllers refer to algorithms that optimize the strength of augmentations throughout training. Some emerging controllers in NLP are AutoAugment, Population-based Augmentation, and RandAugment.
