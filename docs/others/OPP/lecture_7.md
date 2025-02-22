---
comments: true
---

# Lecture 7 - Artificial Intelligence for Decision-Making and Robotics

- Speaker: Dr. Victor-Alexandru Darvariu

## Formulating the Artificial Intelligence Problem

### Intelligent behaviour

The sensorimotor connection provides insights into cause-and-effect relationships and goal achievement.

*Interactions* generate knowledge about the environment and our own capabilities.

*Learning from interactions* is a key idea that underlies nearly all theories of learning and intelligence.

The following discussion focuses on a *computational* approach for learning intelligent behavior through interaction.

### Reinforcement Learning (RL)

The primary goal is to learn how to make optimal decisions in an uncertain environment.

Optimality is quantified by the rewards the agent receives.

Attractive paradigm for representing the Artificial Intelligence problem.

### Markov Decision Process (MDP)

*Markov Decision Processes* (*MDPs*) are a formalisation of sequential decision-making.

Formally defined as a tuple ($\mathcal{S}, \mathcal{A}, \mathcal{P}, \mathcal{R}, \gamma$) containing the *state space*, *action space*, *transition function*, *reward function*, and *discount factor*.

Agent-environment interactions define a *trajectory* $S_{0}, A_{0}, R_{1}, S_{1}, A_{1}, R_{2}, \dots$

The *return* of a trajectory is the discounted sum of rewards: $\sum_{k = 0}^{\infty} \gamma^{k} R_{t + k + 1} = R_{t + 1} + \gamma R_{t + 2} + \gamma^{2} R_{t + 3} + \cdots$

The *policy* $\pi(a|s)$ fully defines agent's behaviour.

The *action-value function* $Q_{\pi}(s, a)$ is the expected return when starting in state $s$, taking action $a$, and following policy $\pi$ thereafter:

$$Q_{\pi}(s, a) = \mathbb{E}_{\pi} \left[ \left. \sum_{k = 0}^{\infty} \gamma^{k} R_{t + k + 1} \right| S_{t} = s, A_{t} = a \right]$$

**Goal**: Find the optimal policy $\pi_{*}$ that satisfies

$$\pi_{*} = \mathop{\text{argmax}}_{\pi} Q_{\pi}(s, a)$$

## Reinforcement Learning Algorithms

### Bellman Optimality Principle

An optimal policy has the property that, regardless of the initial state and initial decision, the remaining decisions must form an optimal policy with respect to the state resulting from the first decision.

- This is a key principle underlying AI algorithms for decision-making.
- It provides a way to *break down* problems into smaller subproblems.
- Optimal behaviour for the entire problem can be achieved by making optimal choices for each subproblem.

### Policy Iteration

This is a general framework for finding the optimal policy, with a variety of applicable methods (Dynamic Programming, Monte Carlo Methods, Temporal-Difference, etc.).

*Q-Learning* (Watkins and Dayan, 1992)

$$Q(s, a) \leftarrow Q(s, a) + \alpha[r + \gamma \mathop{\max}_{\alpha' \in \mathcal{A}(s')} Q(s', a') - Q(s, a)]$$

*Deep Q-learning* leverages neural networks to handle large state and action spaces.

### Model-Free and Model-Based RL

These represent two families of RL algorithms.

Here, "model" refers to knowing the true (or having an estimate of) the transition and reward functions.

Q-learning is a *model-free* algorithm that only requires samples of agent-environment interactions.

*Model-based* algorithms leverage knowledge of transition and reward functions to significantly accelerate learning.

### Solving MDPs by Planning

Using the transition and reward functions, we can *plan* a good action ahead of time, avoiding costly lessons in the real environment.

Construct a *tree* of possible states and actions, then *search* for the optimal action.

The way the tree is built and navigated is dictated by the particular search algorithm.

Search algorithms have been widely used to build intelligent agents since the early days of AI.

### Monte Carlo Sampling

It can stop expanding all possibilities at a certain point in the tree.

Instead, actions can be sampled using a strategy (e.g., uniformly at random).

The value of a state is the average of the rewards obtained from the sampled trajectories.

### Monte Carlo Tree Search

- Selection: Choose the most promising nodes to explore.
- Expansion: Add new nodes to the tree based on selected actions.
- Simulation: Roll out trajectories from the expanded nodes.
- Backpropagation: Update the value estimates based on simulation results.

### Imitation Learning

Learning entirely from scratch (as is typical in RL) can be resource-intensive in certain scenarios.

An alternative approach is to collect expert demonstrations (e.g., from humans or high-performing algorithms) and train a model using supervised learning.

This approach is widely used in robotics.

It was used for driverless cars as early as 1989!

More recent work follows the same principles but leverages more data and better architectures.

Other examples include flying drones, robotic manipulators, and more.

This approach is generally useful for tasks where optimal demonstrations are relatively inexpensive to generate.

## The Role of Neural Networks

Many of the successful methods discussed earlier rely on neural networks. *Why*?

For small-scale problems, the state space can be explicitly enumerated.

In practical RL problems, the state space can grow exponentially large.

> Chess, for example, has approximately $10^{66}$ possible positions. For comparison, the number of atoms on Earth is about $10^{50}$, and the number of atoms in the known universe is about $10^{80}$.

Neural networks can generalise between states that, while distinct, share common characteristics.

### Properties of Neural Networks

Certain classes of neural networks are known as *universal function approximators*.

Informally, given enough data, they can approximate any input-to-output mapping.

For example: the input is an image, and the output is either `cat` or `dog`.

They are widely used for *perception*: transforming *RAW* inputs into meaningful features.

They are also leveraged for *function approximation* of the policy and value functions in RL.

When making decisions, a higher-level algorithmic component is still necessary.

## Applications in Robotics and Beyond

- Ocean Sampling
- Goal-Directed Graph Construction
- Causal Discovery

## Summary

RL is a means of formulating the AI problem that relies on interactions with an environment.

Classes of RL algorithms include model-free RL, model-based RL (planning), and imitation learning.

Neural networks are often used to approximate complex input-to-output mappings.

We also briefly explored applications of these algorithms in marine robotics and network optimization.
