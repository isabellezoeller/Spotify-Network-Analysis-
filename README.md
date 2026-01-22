# Spotify Network-Based Music Recommendation System

A network science approach to generating music recommendations using Spotify audio features. Songs are modeled as nodes connected by audio similarity, and community detection methods are used to create genre-informed “playlists” and identify central artists.

---

## Overview

Instead of relying on collaborative filters or embeddings, this project explores a **purely audio-driven network representation of music**:

- Each song is treated as a **node**
- Edges represent **audio similarity** above a threshold
- Communities correspond to **coherent listening groups/playlists**
- Centrality highlights **influential / bridge-like** songs and artists

This was completed as a final project for **Math 168: Introduction to Networks** and integrates concepts from graph theory, community detection, and recommender systems.

---

## Methodology

### **1. Data**
We used a dataset of **≈98,000 Spotify tracks** with features including:

- `danceability`, `energy`, `valence`, `speechiness`, `acousticness`, `instrumentalness`, `liveness`
- `tempo`, `loudness`
- `genre`, `artist`, `year`, `popularity`

Due to computational cost, a **stratified sample of ~7,000 songs** was drawn to maintain proportional genre coverage.

### **2. Similarity Function**
Audio similarity between two songs was computed using a **weighted combination** of continuous audio features with:

- exponential decay for temporal features (e.g., year, tempo)
- power-law exponents for [0,1] bounded features
- optional weights for genre/popularity matching

An edge is created if:  
`similarity(song_i, song_j) > τ`

### **3. Network Construction**
- Nodes represent songs
- Weighted edges represent similarity
- Resulting graph stored as an edge list for further analysis

### **4. Community Detection**
We used **Louvain modularity optimization** to discover cohesive “listening communities.”

Varying resolution parameters controls community granularity:
- Low resolution → fewer, larger communities
- High resolution → more, smaller communities

### **5. Network Analysis**
We computed classical centrality metrics to identify structurally important songs:

- **Degree centrality**
- **Betweenness**
- **Closeness**
- **Eigenvector centrality**

These help surface **bridge songs**, **genre hubs**, and **stylistic influencers**.

---

## Results & Insights

Key findings from the sampled network:

- The audio-similarity graph exhibits **strong genre clustering**
- Louvain detection produced communities that align with **genres, eras, or moods**
- Centrality rankings surfaced **genre-defining or highly connected tracks**
- Resolution tuning allows constructing playlists by:
  - **Mood** (e.g. sad, party, chill, sleep)
  - **Genre**
  - **Era**
  - **Tempo/Energy profiles**

Example community labels were built from centroid feature vectors (mean audio features per community).

A full report with tables, figures, and appendix lives here:  
 `/NetworkRecommendationReport.pdf`

---

## Repository Structure

```
├── data/                # input CSVs (omitted from repo due to size)
├── figures/             # generated plots (communities, histograms, etc.)
├── src/                 # similarity + network construction code
├── notebooks/           # exploratory analysis + community tuning
├── NetworkRecommendationReport.pdf
└── README.md
```

---

## Tech Stack

- **Python**
- **NetworkX**
- **scikit-learn**
- **Pandas / NumPy**
- **Matplotlib / Plotly**
- **Louvain community detection**


