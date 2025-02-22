---
comments: true
---

# Lecture 18 - The Age of (Healthcare) Big Data: Past, Present, Future

- Speaker: Prof. Bartek Papiez - Big Data Institute, Oxford University

## Early Development

### McCulloch-Pitts Neuron

**Features**

- Binary inputs and outputs ($\{0, 1\}$): The neuron's output is either active ($1$, firing) or inactive ($0$, not firing), with multiple inputs.
- Weights represent the strength of the connection between inputs and the neuron.
- Activation: The neuron fires only if the weighted sum of its inputs surpasses a predefined threshold.

**Limitation**

- The signal is binary.
- The weighting and activation mechanism renders the model non-learnable.
- Not all problems are linearly separable.

### The Perceptron Model by Frank Rosenblatt (1957)

$$f(x) = \left\{
\begin{aligned}
1,\ & \text{if}\ wx + b > 0 \\
0,\ & \text{otherwise}
\end{aligned}
\right.$$

However, linear models cannot solve all problems, as exemplified by the *XOR problem*.

### LeNet-1: The Dawn of Convolutional Neural Networks (1988)

This marked the beginning of the widespread use of Convolutional Neural Networks (CNNs).

## Present

### The ImageNet Revolution (2009)

ImageNet is an image database structured according to the WordNet hierarchy (currently limited to nouns), where each node is represented by thousands of images. This project has significantly advanced computer vision and deep learning research, with data freely available for non-commercial use.

WordNet is a comprehensive lexical database of English, grouping nouns, verbs, adjectives, and adverbs into sets of cognitive synonyms (synsets), each representing a distinct concept.

ImageNet comprises 14,197,122 images organised into 21,841 subcategories, which are further grouped under 27 high-level categories.

### AlexNet: A Breakthrough in Deep Learning (2012)

- Contains 60 million parameters
- A large, deep convolutional neural network capable of achieving record-breaking results
- The network's size is constrained by GPU memory and training time. Training on two GTX 580 3GB GPUs takes five to six days.

### Recent Developments

Generative Pre-trained Transformer 3 (GPT-3), a language model, held the record as the largest neural network with 175 billion parameters (2020).

The Megatron-Turing Natural Language Generation model (MT-NLG) is the largest and most powerful monolithic transformer English language model, with 530 billion parameters (2021).

NVIDIA's Selene supercomputer comprises 560 DGX A100 nodes.

Each cluster node has 8 NVIDIA 80-GB A100 GPUs.

On average, the human brain contains about 100 billion neurons.

Each neuron may be connected to up to 10,000 other neurons, passing signals to each other via as many as 1,000 trillion synapses.

The Pathways Language Model (PaLM) achieved breakthrough performance with 540 billion parameters (2022).

GPT-4: Due to competitive and safety considerations, details about its architecture, hardware, training compute, dataset construction, and methods are not disclosed.

## Applications of AI in Medicine

### Deep Learning in Medical Imaging

Deep neural networks achieve dermatologist-level accuracy in skin cancer classification.

CheXNet: Deep learning enables radiologist-level pneumonia detection in chest X-rays.

### Generative Models in Artificial Neural Networks

Image generation pipeline: Prompt -> Text encoder ->Diffusion process -> Image decoder -> Output

### AI Applications During the COVID-19 Pandemic

Conventional data analysis has been central to the COVID-19 response, rather than AI.

While innovative AI applications emerged during the pandemic, evidence indicates that traditional data collection and analysis methods were more widely used.

Despite significant efforts to develop machine learning models for COVID-19 diagnosis and prognosis, methodological flaws and biases in the literature led to overly optimistic performance reports.

Chellenges of Medical Imaging in Healthcare: AI algorithms can be *black-box*.

### Explainable AI for Medical Imaging

How can we extract NLEs from raw radiology reports?

The findings and impression sections, containing descriptive content, are extracted first. Labels and sentences with explanation keywords are then identified.

### The Role of AI in Healthcare: Opportunities and Challenges

It is crucial to ensure that the development of clinical AI is guided by principles of trust and explainability.

Measuring AI medical knowledge against that of expert clinicians is a critical step in evaluating trust and explainability.

The performance of ChatGPT was evaluated on the United States Medical Licensing Exam (USMLE).

The USMLE is a set of three standardized tests of expert-level knowledge, which are required for medical licensure in the United States.

ChatGPT performed at or near the passing threshold of 60% accuracy.

As the first to achieve this benchmark, ChatGPT marks a notable milestone in AI maturation.

The novel workflow of **AI as Supporting Reader** maintains screening performance comparable to human double reading while significantly reducing workload and enhancing safety.

Disruptive technology can democratise knowledge and power, yet also polarise, amplify biases, and exacerbate inequalities, depending on its deployment and use.

Large language models will further blur the distinction between truth and falsehood, particularly in areas with weak evidence, scarce information, or ongoing debate.
