---
comments: true
---

# Lecture 19 - The Changing Faces of Deepfakes and Generative AI

- Speaker: Prof. Bernie Hogan - Associate Professor and Senior Research Fellow

## Likeness

A *likeness* is not so much a tangible entity as it is a relational construct.

A photograph may be authentic or fabricated; however, if it is fabricated yet "contains a likeness," this implies a connection between the real individual and the depicted subject.

Conversely, a genuine photograph of an individual may be of poor quality or blurred, making it challenging to ascertain their identity. In such cases, the photograph may lack the individual's likeness.

However, likeness is not a stable attribute but rather a relational one.

- There is no definitive or 'true' likeness; rather, it exists on a spectrum of similarity to its referent.
- As the referent evolves over time, so too does the likeness.

## Sufficient Likeness

To define a sufficient condition ($P = Q$):

- If $P$ is recognisable within the image and the image incorporates features derived from data pertaining to $P$, then the image embodies $P$'s likeness ($Q$).
- In other words, $Q$ satisfies a *recognition threshold*.
- $P$ might be a specific person (e.g., Barack Obama).
- $P$ might represent a category of individuals (e.g., people, Black Americans, Facebook users).

This concept is not exclusive to generative media:

- An artist may depict $P$ by employing her as a model or utilising her photograph.
- Similarly, an artist might render *people* or *trees* in a generalised manner rather than depicting a specific individual or tree.

## Differences between Deepfake and Sunthetic Media

A *synthetic image* refers to an image generated through an image model.

A *deepfake* constitutes an image, audio, or video file that employs a model to produce a specific likeness.

A *likeness* constitutes an abstraction derived from source material, representing a specific individual.

The quality of a likeness, whether **well or poorly learned**, determines the extent to which a synthetic image can accurately represent an individual.

What defines a sufficient likeness, and for what purpose? How does this apply in political contexts?

A sufficient likeness need not exhibit realism; rather, it necessitates contextual relevance.

## Uncanny Valley

A characteristic of an image or video that approximates realism without fully achieving it.

Consider the following images: while some exhibit similarity, others evoke an *uncanny* quality.

The term "valley" is used because individuals tend to prefer images that either closely resemble or significantly differ from a known person, while those in between elicit discomfort.

## The Stable Diffusion UNet

A UNet processes an initial image derived from random noise by applying convolutional operations, steering mechanisms, and incremental noise addition at each stage.

This simplified U-Net architecture involves downsampling the image, passing it through a bottleneck, and subsequently upsampling it.

Throughout this process, the document is guided by *embeddings*, which represent vectorised textual data. Although derived from text, these embeddings are not essential for the system's functionality.

## Conditioning: Embeddings

Transformers employ attention mechanisms to focus on specific textual elements, which are subsequently converted into numeric representations.

Currently, most models utilise variants of CLIP or T5.

### Mechnism

TThe embeddings do not generate the image directly but rather guide it towards a conceptual understanding. For instance, using the word "cat" results in an image that remains "cat-like" despite variations arising from differing initial conditions.

### Relative Distance

Embeddings suggest that words possess a *relative distance* within the vector space.

This distance is typically quantified using *cosine similarity*, a metric that measures relative distances within a high-dimensional connection space.

Below, $A$ and $B$ denote two vectors, representing the connections between **cat** and all other nodes, and **dog** and all other nodes, respectively.

$$\cos \theta = \frac{A \cdot B}{\|A\| \|B\|} = \frac{\sum_{i = 1}^{n} A_{i} B_{i}}{\sqrt{\sum_{i = 1}^{n} A_{i}^{2}}\sqrt{\sum_{i = 1}^{n} B_{i}^{2}}}$$

The cosine distance between two vectors is thus:

$$d_{\cos} = 1 - \cos \theta = 1 - \frac{A \cdot B}{\|A\| \|B\|}$$

### Different Training Data

Different embeddings result in varying conceptual proximities based on their positions within the embedding space. Introducing new training data can alter these proximities, causing some concepts to converge or diverge.

## Key Takeaway

Generative imagery remains inherently unstable and difficult to control, despite its ease of generation. Such media primarily serves to evoke imagery rather than convey factual information.

Our focus should centre on the capacity to evoke specific subjects (or objects) rather than the factual accuracy of the evoked content.
