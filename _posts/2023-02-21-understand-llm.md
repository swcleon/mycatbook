---
title: Understanding the Capabilities, Limitations, and Societal Impact of Large Language Models
categories: [all, nlp]
comments: true
usemathjax: true
---

[Tamkin, Alex et al. ArXiv abs/2102.02503 (2021): n. pag.](https://arxiv.org/pdf/2102.02503.pdf)

## Introduction

On October 14th, 2020, researchers from OpenAI, the Stanford Institue for HCAI, and other universities discuss about GPT-3 regarding two main questions:

- What are the technical capabilities and limitations of large language models?
- What are the societal effects of widespread use of large language models?

## Technical Capabilities and Limitations

About the scale of GPT-3:

- Growth in model capabilities as they scale "feels like a law of physics or thermodynamics" in its stability and predictability.
- Training such a large language model requires many people with diverse backgrounds to continuously interrogate the model's capabilities for possible problems (e.g., bias, misuse, safety concerns, etc.).

About the understanding of GPT-3:

- Getting things "mostly right" may not be sufficient for understanding if the model performs poorly on rare but important inputs.
- Models that truly understand should grasp the causal relationship between features of the data and the desired behavior. With enough data, language models could encounter "natural experiments" that could enable the model to learn causal relationships from observational data in a similar manner as human economists often do in their reserach.
- Perhaps understanding is not the correct focus since humans are able to accomplish many tasks with mediocre or even poor understanding.

About the Multimodality of GPT-3:

- In a way, GPT-3 is already trained on multimodal data since the training data contains prose, structured data tables, and computer code.
- Shortly after this workshop, OpenAI released DALL-E, which is a multimodal version of GPT-3 trained on both images and text.

About the Alignment of GPT-3:

- Aligning human and model objectives was seen to be especially important for "embodied" AI agents which learn through active interaction with their environment.

## Effects of Widespread Use

About the Capabilities of GPT-3:

- A large set, including text summarization, chatbot behavior, search, code generation, and essay generation.
- Thus increasing the difficulty to provide model access to support a large community to red-team (interrogate the model for potential misuse and develop mitigation strategies).

About the deployment of GPT-3:

- Increase the conputing resources available to academia so that it would be easier for academics to do research.
- Laws requiring disclosure of when AI is being used to generate text could be helpful in managing the effects of large language models.
- Those on the cutting edge should use their position on the frontier to responsibly set norms in the emerging field.

About the disinformation of GPT-3:

- Models like GPT-3 can be used to create false, misleading, or propagandistic essays, tweets and news stories de novo.
- Empirically investigating the economics of automated vs. human generated disinformation is important.
- GPT-3 or other future language models could make disinformtion hard or impossible to detect at the level of content, forcing reliance on metadata by online platforms.

About the bias of GPT-3:

- It is difficult to define what is means to mitigate bias in large language models ina universal manner, since appropriate language use is highly contextual.
- All datasets are biased in some ways, so the challenge is not eliminating all bias but addressing harmful biases according to some set of normative and/or legal criteria.
- Possible means of addressing harmful biases in language models:
  - Changes to the initial training data to mitigate bias a prior.
  - Training a separate model to filter content generated by a language model.
  - Fine-tuning a large language model on data with desired properties.
  - Tagging data so that the model learns to distinguish among certain forms of content.
  - Training models to be more "fact-aware".
  - Reinforcement learning with human feedback.
  - Leveraging the model's own knowledge to improve outputs (e.g., with careful prompt design).
  - Developing more expansive suites of "bias tests" that models can be run through prior to deployment.
  - Red-teaming the model at scale by engaging trusted partners to work with the model and through limited commercial offerings.
- Keeping a human in the loop of text generation is critical for addressing the bias issue.

## Future Research Directions

- Can we better understand why language models improve so much with scale? Can this enable us to build models which scale more efficiently?
- What are the limits of scaling? Will scale lead to strong causal reasoning symbolic manipulation, commonsese understanding, and robustness to a wider class of inputs? Or will different techniques be necessary?
- How can we develop new neural network architectures and algorithms that enable efficient learning from diverse, multimodal data beyong text?
- What are the opportunities and tradeoffs involved in different approaches to steering the outputs of large-scale language models to be more aligned with human values?
- How should access to models like GPT-3 be allocated, balancing considerations like security, replicability, and fairness? What kinds of tests do we need to develop in order to qualify language models like GPT-3 as being safe or unsafe for use in particular contexts?
- What can academia do to best position itself to develop guardrails for the industrial development of such models - including advocating for sufficient funding to replicate the compute resources required to train them?
- How can we best foster cross-disciplinary collaboration to understand and manage the biases in large datasets and model representations of such datasets?
- How can be best characterize the potential "threat landscape" for such models; e.g., do we need to spend more time worrying about how models like this could be used by profit-driven actors to generate lots of low-grade spam, or should we be more worried about state-based actors using models to generate persuasive text for use in disinformation campaigns?
- How cost-effective and skill-intensice would it be for malicious actors to misuse language models for various puurposes, compared to alternative methods of achieving the same goals?