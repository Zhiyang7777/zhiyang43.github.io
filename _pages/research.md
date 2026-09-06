---
title: "Research"
permalink: /research/
layout: single
author_profile: true
toc: true
toc_label: "On this page"
toc_sticky: true
---

My research lies at the intersection of signal processing and machine learning on graphs and geometric data, spanning graph signal processing, graph neural networks, geometric data analysis, wireless communications, and scalable autonomous systems. The common goal is to understand deep learning on real-world geometric data well enough to say why it works and when it fails: to characterize its mathematical foundations, and to use that understanding to design new architectures and training procedures.

One recurring tool is the limit perspective, which treats a graph as a finite sample of a continuous object such as a manifold or a graphon. This turns stability, generalization, and transfer across graph sizes into questions about convergence. The three threads below are where this program has produced the most so far. I am also interested in how far these ideas carry into other domains, including medical and brain imaging, robotic and multi-agent systems, chip design, and reasoning over knowledge graphs.

---

## Properties of GNNs via a Manifold Limit

Point clouds, sensor networks, meshes, and similarity graphs built from high-dimensional features are finite samples of a smooth low-dimensional surface, a manifold. As more points are sampled, a GNN on the graph behaves more and more like a continuous operator on that surface. Studying the continuous operator tells us what the GNN can and cannot do, independently of how many points were sampled.

<figure class="align-center">
  <img src="/assets/images/research/research-manifold.png" alt="Geometric graphs sampled from a manifold with increasing n, converging to the manifold limit">
  <figcaption>Geometric graphs sampled from a 2-D manifold at increasing resolution. The node colors show a graph Laplacian eigenvector; as <em>n</em> grows it converges to the corresponding Laplace–Beltrami eigenfunction of the manifold, and a GNN on the graph converges to a <em>manifold neural network</em>.</figcaption>
</figure>

We define *manifold filters* as functions of the Laplace–Beltrami operator and build *manifold neural networks* (MNNs) by composing them with pointwise nonlinearities, the continuous analogue of graph filters and GNNs. Three families of results follow.

- *Convergence.* GNNs on geometric graphs constructed from manifold samples converge to MNNs as the number of sampled points grows, with non-asymptotic rates. This holds both for dense graphs and for *relatively sparse* graphs, where the connectivity radius shrinks with the sample size.
- *Stability versus discriminability.* Manifold filters are stable to deformations of the underlying manifold, but only if their frequency response is not too sharp. Filters that separate nearby Laplacian eigenvalues are the ones most sensitive to perturbation; the nonlinearity in an MNN recovers discriminability without giving up stability.
- *Statistical generalization.* Viewing training graphs as samples from a manifold gives generalization bounds for GNNs that decrease with the number of nodes and depend on the intrinsic dimension of the manifold rather than the graph size. The bounds are robust to model mismatch (a GNN trained on graphs from one manifold generalizes to graphs from a deformed version of it) and extend to Lipschitz losses.

**Key papers**

- Z. Wang, J. Cerviño, A. Ribeiro. *A Manifold Perspective on the Statistical Generalization of Graph Neural Networks.* ICML 2025. [[arXiv]](https://arxiv.org/abs/2406.05225)
- Z. Wang, J. Cerviño, A. Ribeiro. *Generalization of Graph Neural Networks is Robust to Model Mismatch.* AAAI 2025. [[arXiv]](https://arxiv.org/abs/2408.13878)
- Z. Wang, J. Cerviño, A. Ribeiro. *Generalization of Geometric Graph Neural Networks with Lipschitz Loss Functions.* IEEE Trans. Signal Processing, 2025. [[arXiv]](https://arxiv.org/abs/2409.05191)
- Z. Wang, L. Ruiz, A. Ribeiro. *Geometric Graph Filters and Neural Networks: Limit Properties and Discriminability Trade-offs.* IEEE Trans. Signal Processing, 2024. [[arXiv]](https://arxiv.org/abs/2305.18467)
- Z. Wang, L. Ruiz, A. Ribeiro. *Stability to Deformations of Manifold Filters and Manifold Neural Networks.* IEEE Trans. Signal Processing, 2024. [[arXiv]](https://arxiv.org/abs/2106.03725)
- C. Battiloro, Z. Wang, H. Riess, P. Di Lorenzo, A. Ribeiro. *Tangent Bundle Convolutional Learning: from Manifolds to Cellular Sheaves and Back.* IEEE Trans. Signal Processing, 2024.
- C. F. Deberaldini Netto, Z. Wang, L. Ruiz. *Improved Image Classification with Manifold Neural Networks* (ICASSP 2025) and *Graph Semi-Supervised Learning for Point Classification on Data Manifolds* (arXiv 2506.12197).

---

## Size Generalization of GNNs

A GNN has the same number of parameters regardless of the number of nodes, so a model trained on graphs with a few hundred nodes can be run on graphs with millions. Size generalization, or transferability, asks when and how fast the output of a fixed GNN stabilizes as the graph grows, so that small graphs suffice for training and large graphs need no retraining.

<figure class="align-center">
  <img src="/assets/images/research/research-size.png" alt="One GNN with fixed weights applied to graphs of increasing size sampled from a common limit model; the transfer error decays with graph size">
  <figcaption>Graphs of different sizes drawn from a common limit model (a graphon or a manifold) are processed by <em>one</em> GNN with a single set of weights. The difference between its outputs on two such graphs is bounded by a quantity that vanishes as both graphs grow — so training on small graphs and deploying on large ones is justified.</figcaption>
</figure>

The approach is to identify a limit object that graphs of every size approximate, show that the GNN converges to its limit counterpart, and bound the difference between any two finite graphs by their distances to the limit. For graphons and manifolds this gives:

- *Transferability bounds* for graph filters and GNNs across dense graphs (graphon limits) and across geometric graphs of increasing resolution (manifold limits), including the relatively sparse regime, where the transfer error is controlled by the connectivity radius as well as the number of nodes.
- *Graphon pooling*, which coarsens graphs and graph signals consistently with the limit, so that multi-resolution architectures remain transferable.
- *Stability of aggregation GNNs*, which process a graph by repeated local diffusion followed by a standard neural network. The architecture is naturally decentralized, and we characterized its stability to graph perturbations.
- *Transferability on sparse random geometric graphs.* Most transferability guarantees assume dense graphs whose node degrees grow with the network, which is not the case for wireless and other spatial networks. We gave a transferability theory for GNNs on random geometric graphs, a sparse model in which degrees stay bounded as the network grows, which matches the transfer observed empirically for GNN wireless policies.
- *Size transferability of graph transformers.* Attention-based models are not transferable on their own; they inherit size transferability from convolutional positional encodings, which makes transformers usable on very large geometric graphs.

**Key papers**

- R. Garcia Camargo, Z. Wang, A. Ribeiro. *Graph Neural Networks in Large Scale Wireless Communication Networks: Scalability Across Random Geometric Graphs.* ICASSP 2026. [[arXiv]](https://arxiv.org/abs/2510.00896)
- J. Porras-Valenzuela, Z. Wang, X. Shang, A. Ribeiro. *Size Transferability of Graph Transformers with Convolutional Positional Encodings.* Preprint, 2026. [[arXiv]](https://arxiv.org/abs/2602.15239)
- Z. Wang, L. Ruiz, A. Ribeiro. *Geometric Graph Filters and Neural Networks: Limit Properties and Discriminability Trade-offs.* IEEE Trans. Signal Processing, 2024. [[arXiv]](https://arxiv.org/abs/2305.18467)
- A. Parada-Mayorga, Z. Wang, A. Ribeiro. *Graphon Pooling for Reducing Dimensionality of Signals and Convolutional Operators on Graphs.* IEEE Trans. Signal Processing, 2023. [[arXiv]](https://arxiv.org/abs/2212.08171)
- A. Parada-Mayorga, Z. Wang, F. Gama, A. Ribeiro. *Stability of Aggregation Graph Neural Networks.* IEEE Trans. Signal and Information Processing over Networks, 2023.
- L. Ruiz, Z. Wang, A. Ribeiro. *Graph and Graphon Neural Network Stability.* ICASSP 2021.

---

## GNNs in Wireless Communication Networks

A wireless network is a graph whose edges are interference: transmitters sharing the spectrum are neighbors, and the edge weights are fading channel gains. Deciding who transmits, at what power, and on which channel is a non-convex problem that must be re-solved whenever the channels change. GNNs turn this into a learning problem, with a policy that maps the channel state directly to an allocation. Built from local graph operations, the policy is decentralized; being permutation-equivariant, it does not depend on how users are labeled or how many there are.

<figure class="align-center">
  <img src="/assets/images/research/research-wireless.png" alt="Interference graph of transmitter–receiver pairs, learned power allocation, and the same policy applied to a larger network">
  <figcaption>Left: an ad-hoc network as an interference graph (solid: direct links; dashed: interfering channels). Center: a GNN policy maps channel gains to transmit powers. Right: the same policy, with the same weights, deployed on a larger network without retraining.</figcaption>
</figure>

We parameterize the allocation policy with a decentralized *aggregation GNN* (Agg-GNN): each node collects channel and state information from its neighbors through a few rounds of local exchanges over the network itself, and a neural network maps the aggregated sequence to its own decision. The policy is trained with a primal–dual method that needs no labeled optimal allocations, only the utility and the constraints. The resulting policies:

- match or beat classical heuristics and optimization baselines on sum-rate and constrained problems, at a fraction of the computation;
- are *decentralized* by construction, using only information that can actually be exchanged over the wireless links, and extend to *asynchronous* operation where nodes update at different times with delayed information;
- are *stable and transferable*: viewing dense networks as samples from a manifold shows that policies trained on small networks remain near-optimal on larger and denser ones, and recent work analyzes this scalability directly over random geometric graphs.

Follow-up work covers link scheduling with *state-augmented* GNNs (which enforce long-term constraints by augmenting the input with dual variables), and learning-based routing and scheduling in heterogeneous industrial IoT networks.

**Key papers**

- Z. Wang, M. Eisen, A. Ribeiro. *Learning Decentralized Wireless Resource Allocations with Graph Neural Networks.* IEEE Trans. Signal Processing, 2022. [[arXiv]](https://arxiv.org/abs/2107.01489)
- Z. Wang, L. Ruiz, M. Eisen, A. Ribeiro. *Stable and Transferable Wireless Resource Allocation Policies via Manifold Neural Networks.* ICASSP 2022. [[arXiv]](https://arxiv.org/abs/2110.04706)
- R. Garcia Camargo, Z. Wang, A. Ribeiro. *Graph Neural Networks in Large Scale Wireless Communication Networks: Scalability Across Random Geometric Graphs.* ICASSP 2026. [[arXiv]](https://arxiv.org/abs/2510.00896)
- R. Garcia Camargo, Z. Wang, N. NaderiAlizadeh, A. Ribeiro. *Wireless Link Scheduling with State-Augmented Graph Neural Networks.* Asilomar 2025.
- Z. Wang, J. Guo, K. Parsons, Y. Nagai, T. Sumi, P. Orlik. *Learning Based Routing Link Scheduling in Heterogeneous Wireless IoT Networks.* IEEE ICC Workshops, 2024.

---


