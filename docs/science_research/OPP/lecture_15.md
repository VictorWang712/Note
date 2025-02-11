---
comments: true
---

# Lecture 15 - Social Networks from Math to Measurement

Speaker: Prof. Bernie Hogan - Associate Professor and Senior Research Fellow

The concept of networks predates the Internet.

The mathematical foundations of networks originate from graph theory, exemplified by the *Königsberger Brückenproblem* (Seven Bridges of Königsberg).

## Fundamental Concepts in Network Theory

- **Node** ($v_{i}$): An individual entity represented as a *vertex*. Nodes can represent people, countries, books, etc., but should be of the same *mode* (e.g., all nodes are people).
- **Edge** ($e_{ij}$): A connection or association between two nodes, $v_{i}$ and $v_{j}$.
- **Graph** ($G$): A formal representation of a network as a collection of nodes and edges.
- **Degree**: The number of edges incident to a node, often interpreted as the number of connections or friendships.

Colloquial terms such as *actor* or *user* may be used to refer to nodes, while *tie* or *link* may denote edges.

## Modelling Emergent Properties Through Networks

Emergent properties arise not from deliberate design but from the interactions and organisation of agents within a system.

For instance, diamonds emerge from the highly ordered, grid-like arrangement of carbon atoms.

Thunderstorms result from the chaotic, turbulent heating of moisture in the atmosphere.

Social networks exhibit both order and chaos, as individuals form connections within specific constraints and based on personal preferences.

> Gephi: A Tool for Network Visualisation and Analysis
>
> Gephi is an open-source, cross-platform software designed for network visualisation and basic analysis.
>
> [Gephi - The Open Graph Viz Platform](https://gephi.org/)

Below is an illustrative example to demonstrate the application of the discussed principles.

> Emergent Polarisation in Political Blogs
>
> The study *Divided they Blog* by Adamic and Glance analysed political blogs in 2004, categorising them as Democrat (blue) or Republican (red).
>
> Data comes from: [Network data](https://public.websites.umich.edu/~mejn/netdata/)
>
> Initially, the blogs appear randomly distributed.
>
> However, analysing the linking patterns reveals a clear structure of polarisation.

## Technical Aspects of Community Detection

Community detection identifies groups of nodes with a higher density of internal connections compared to external ones.

Modularity ($Q$) is a metric that quantifies the quality of community structure within a network.

- $Q < 0$: Indicates that nodes within a group are more likely to connect outside their group.
- $Q \sim 0$: Suggests no preference for intra-group connections.
- $Q \geq 0.3$: Indicates a strong preference for intra-group connections.

> In the study *Divided they Blog*, $Q \sim 0.43$.

If *ground truth* data is available, misclassification rates can be calculated to evaluate community detection accuracy.

> CDLib package in Python is useful for this. See: [CDlib_tutorial.ipynb - Colab](https://colab.research.google.com/github/KDDComplexNetworkAnalysis/CNA_Tutorials/blob/master/CDlib_tutorial.ipynb)

## Transitioning from Macro Networks to Ego Networks

Ego networks enable the study of individual nodes within a larger population.

This approach is particularly useful when the complete network is unknown, and accurate analysis through trace data is impractical.

The term **ego** refers to the focal node or respondent in the network.

The term **alter** denotes all other nodes connected to the ego.

Visualising ego networks can lead to cluttered diagrams due to the density of connections.

## Future Directions in Network Analysis

On the web, networks are instrumental in understanding information diffusion, diversity, and generating recommendations.

Networks can be constructed to map interactions, such as individuals replying to each other online.

- For instance, under a Bilibili video: Do the same users comment across multiple videos? How can this information be used to map online communities?
- Analysing regular behaviour in health-related forums: Are certain individuals dominant? Do they interact primarily with each other or with newcomers?

In-person networks remain valuable for studying meaningful relationships, with tools like Network Canvas facilitating analysis.

## The Concept of Universal Connectivity

In 1968, Milgram and Travers conducted a study known as the *Six Degrees of Separation*.

The study involved sending packages from randomly selected individuals in Nebraska to a target person at MIT.

On average, the packages required six intermediaries to reach the target (if they arrived at all).

Recent research suggests that the number of degrees of separation may be even smaller, with individuals potentially connected to anyone in the world in just four or five steps.
