# Lecture 4 - Geometric Deep Learning: Part 1

- Speaker: Dr. Elena Gal

## Deep Learning

**Setup**

Set of observations or samples $\mathcal{D} = \{(x_{i}, y_{i})\}^{N}_{i = 1}$ drawn *i.i.d.* from distribution $P$ over $x \times y$.

Coordinates of $x \in \mathcal{X} = \mathbb{R}^{\text{d}}$ are called features, and elements of $y$ are labels.

We assume the existence of a function $f$ *s.t.* $y_{i} = f(x_{i})$.

**Goal**

Approximate $f$ by functions from class $\mathcal{F} = \{ f_{\theta \in \Theta} \}$.

## Deep Neural Network - Multilayer Perceptrons

Multilayer Perceptrons are the simplest example of Deep Neural Networks.

Each layer consists of $z = \theta^{T}x$ and a non-linear activation function $\sigma(z)$.

$\theta \in \Theta$ are network parameters or weights.

$\mathcal{R}(\tilde{f}) := \text{E}_{P} L (\tilde{f}(x), f(x))$.

$L$ is a loss function.

For example, $L(y, y') = \frac{1}{2}|y - y'|^{2}$.

## Deep Neural Network - Convolutional Neural Networks

CNN is another architecture for Deep Neural Networks. CNN uses shared *kernels*. A small window slides over the image, and element-wise multiplication is performed between the kernel and the input, followed by taking $\sum$.

CNN architecture facilitates shift-invariant classification (It does not matter where the object is in the image!).

## Social Media, Protein Molecules, and Graph Neural Networks

A *graph* is an object consisting of *vertices* and *edges*.

*Features* are neighbours of each node.

Typical tasks are graph classification, node classification, link prediction, etc.

Graph Neural Networks (GNNs) facilitate *permutation-invariant* classification (Ordering of the neighbours is not important).

## Transformers, Attention, and Large Language Models

An architecture designed to process a connected set of units - e.g., the words in a sentence. The interaction between units is captured through the *attention mechanism*.

LLMs such as ChatGPT and DeepSeek are based on Transformer architecture.

The underlying mathematical concepts are those of a *set* and *inner product*.

## Curse of Dimensionality

Modern Machine Learning datasets often contain hundreds of features, *i.e.*, $\mathbb{R}^{d}$ is a high-dimensional vector space.

*Curse of dimensionality* is a mathematical phenomenon that postulates that the number of samples needed to estimate a function $f: \mathbb{R}^{d} \rightarrow \mathbb{R}$ grows exponentially with the dimension $d$.

**Mathematical Intuition**

$d(v, w) := \sqrt{\sum_{i=1}^{n}(v_{i} - w_{i})^{2}}$

For distinct vectors $v, w$, distance increases with the number of dimensions since each dimension adds a non-negative term to the sum. To maintain the same density, we need exponentially more observations as the dimension increases.

Consider a hypersphere of radius $1$, $S_{n}$, inside a 1-hypercube $C_{n}$. As the dimension $n \rightarrow \infty$ we have

$$\frac{V(S_{n})}{V(C_{n})} = \frac{V(S_{n})}{1} = \frac{\pi^{\frac{n}{2}}}{2^{n} \Gamma(\frac{n}{2} + 1)} \rightarrow 0$$

As the dimension increases, most of the data points are concentrated in the corners of the cube, far from the mean and from each other.

## Geometric Priors, Symmetry, and Scale Separation

The curse of dimensionality implies that learning from generic high-dimensional data is impossible. Therefore, Deep Learning succeeds in applications by approximating specific classes of functions rather than generic ones.

The classes of functions considered in deep learning applications obey laws of geometry and symmetry. These same symmetries inform the design of popular deep learning architectures.
