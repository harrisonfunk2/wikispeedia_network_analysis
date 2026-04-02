# Wikispeedia Network Analysis

A social network analysis project studying the structure of the **Wikispeedia** hyperlink network using **R** and **igraph**.

## Overview

Wikispeedia is an online game where users try to navigate from one Wikipedia article to another using only hyperlinks within the articles. In this project, we model the Wikispeedia article link system as a directed network, where:

- **nodes** represent Wikipedia articles
- **directed edges** represent hyperlinks from one article to another

Using tools from social network analysis, we explored the overall structure of the network, identified highly central articles, examined community structure, and tested whether the observed communities were stronger than what would be expected in random networks.

## Project Goals

The main goals of this project were to:

- visualize the structure of the Wikispeedia network
- analyze whole-network, node-level, and edge-level metrics
- identify important hub and bridge articles
- detect communities of related articles
- examine adjacency matrix patterns before and after node reordering
- statistically validate whether the observed community structure was stronger than random chance

## Dataset

This project uses the **Wikispeedia** dataset from the Stanford Network Analysis Project (SNAP).

The network analyzed in our report contains:

- **4,592 nodes**
- **119,882 directed edges**

We primarily used:

- `links.tsv` to construct the directed graph
- `categories.tsv` to label articles by top-level category

## Methods

Our analysis included the following steps:

### 1. Data Preparation
- Loaded the Wikispeedia data in R
- Constructed a directed `igraph` object from the hyperlink network
- Assigned article categories as node attributes

### 2. Subgraph Visualization
- Sampled **four induced subgraphs** of 200 nodes each
- Visualized the subgraphs using three layouts:
  - **Fruchterman-Reingold**
  - **Kamada-Kawai**
  - **Circular**
- Colored nodes by Wikipedia category and scaled node size by degree

### 3. Network Metrics
We computed several structural metrics, including:

- density
- reciprocity
- clustering coefficient
- assortativity
- diameter
- average path length
- in-degree
- betweenness centrality
- eigenvector centrality
- edge betweenness

### 4. Community Detection
We compared three community detection methods on an undirected version of a sampled subgraph:

- **Fast Greedy**
- **Louvain**
- **Walktrap**

We then examined the modularity scores and compared the detected communities to the article categories.

### 5. Adjacency Matrix Analysis
We examined the adjacency matrix before and after reordering nodes by community membership to see whether clearer block structure emerged.

### 6. Monte Carlo Null Model Test
To test whether the detected community structure was meaningful, we:

- computed Louvain modularity on the full undirected network
- generated **1,000 Erdős-Rényi random graphs** with the same number of nodes and edges
- compared the observed modularity to the null distribution

## Key Findings

Some of the main findings from the project were:

- The network is **sparse** but still shows **short path lengths**, with a diameter of 9 and an average path length of 3.18 in the largest strongly connected component.
- The in-degree distribution is **heavy-tailed**, meaning a small number of articles receive many incoming links while most receive relatively few.
- The article **`United_States`** was the most central article across multiple measures, including in-degree, betweenness, and eigenvector centrality.
- Community detection methods produced similar results, and **Louvain** achieved the highest modularity among the methods compared on the sampled subgraph.
- Reordering the adjacency matrix by community membership revealed visible **block structure**, supporting the presence of meaningful communities.
- In the Monte Carlo null-model test, the observed modularity (**Q = 0.3722**) was far larger than the modularity values from the random graphs, providing strong evidence that the community structure was not due to random chance.
