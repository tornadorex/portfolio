---
layout: default
title: DNS Sinkhole
gh: clustering.md
---

# Clustering Algorithms

The Data Platform uses two different methods to divide a data network into clusters. This article provides an overview of each method and how you can choose one to use when generating a network.

## How are Clusters Generated?

The Data Platform supports two different algorithms for grouping communities of nodes into clusters when visualizing a network: Louvain and OSLOM. Both methods attempt to divide the network into clusters and sub-clusters, but with different goals and end results.

The Louvain algorithm is a fast and efficient method for detecting communities in large networks. It works by repeatedly moving individual nodes between clusters in a way that maximizes the density of the cluster. It’s a widely used method and is considered one of the best algorithms for dividing large networks into clusters, in part because it’s fast and consistent.

OSLOM (Order Statistics Local Optimization Method) is also a community detection algorithm, but it is better suited for identifying hierarchical structures in networks, where clusters are nested within other clusters. This algorithm is also able to detect overlapping clusters, which means that some nodes can be part of more than one cluster.

In general, Louvain can be used for any kind of network, and it’s a good choice when you want to quickly generate clusters in a large network. OSLOM is best used when you expect there to be hierarchical or overlapping clusters in your network, and you want to identify them specifically. The Data Platform uses Louvain by default, but you can use advanced settings to select OSLOM to create a new network.

## Choosing an Algorithm when Generating a Network

On the project page:

1. Click the kebab button to the right of the search you want to visualize.
2. Select **Create Network**.
3. On the Create Network overlay, select the **Clustering Algorithm** you want to use.
4. Adjust the **Ngrams per Label** as necessary.
5. Click **Create** and wait for The Data Platform to generate the network.
