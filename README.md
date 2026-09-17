# FMA Music Dataset Analysis

## About the Dataset

The **Free Music Archive (FMA)** is a public dataset containing approximately **106,574 Creative Commons audio tracks** released by Defferrard et al. (2017).

The dataset was created to support **music information retrieval research** and contains:

- Artist information
- Album information
- Track titles
- Top-level genres
- Release dates
- 518 pre-computed audio features

The audio features include:

- `MFCC`
- `Chroma`
- `Spectral Centroid`
- `Spectral Bandwidth`
- `Spectral Rolloff`
- `Spectral Contrast`
- `RMSE`
- `Zero Crossing Rate (ZCR)`
- `Tonnetz`

The FMA dataset is organised into three main subsets:

- `small` — 8,000 tracks
- `medium` — 25,000 tracks
- `large` — 106,574 tracks

The analysis in this project mainly uses the **metadata and pre-computed audio features** rather than the raw audio files.

---

## Project Overview

This project analyses the **Free Music Archive (FMA)** dataset from both an audio-feature and metadata perspective.

The analysis is divided into three main sections:

### 1. Per-Decade PCA + K-Means

For each decade with enough observations, the audio-feature space is reduced to two dimensions using `PCA`.

`K-Means` clustering is then applied to the PCA representation.

The goal is to investigate:

- The structure of the audio-feature space
- Differences between decades
- The relationship between genres
- Whether clear clusters exist in the audio data

### 2. Title & Genre Exploration

This section focuses on textual and metadata information from the dataset.

It includes:

#### 2.1 Genre Trend Over Time

The share of each top genre is analysed over time.

This helps investigate how the composition of the FMA catalogue changes across different years.

#### 2.2 Vocabulary by Decade

The most frequent words appearing in song titles are analysed for different decades.

This provides an overview of how title vocabulary changes over time.

#### 2.3 Title Duplication Over Time

The project measures how frequently song titles are repeated within different decades.

This can reveal changes in naming conventions and catalogue density.

#### 2.4 Genre Vocabulary Overlap

The vocabulary of different genres is compared using **Jaccard similarity**.

This measures how much the title vocabulary of two genres overlaps.

### 3. Genre-Pair PCA Centroid Distances Over Time

A global `PCA` is fitted using the standardised audio features.

Tracks are then grouped into five-year periods.

For every genre and period, a centroid is calculated in the two-dimensional PCA space.

The Euclidean distance between genre centroids is then measured over time.

The main research question is:

> **Are genre pairs converging or diverging in audio-feature space over time?**

---

# 1. Per-Decade PCA + K-Means

For each decade containing at least `30` tracks, the standardised FMA audio features are analysed using `PCA`.

`K-Means` clustering is applied to the two-dimensional PCA representation.

The optimal number of clusters is investigated using **elbow detection**.

## Results

Only three decades contain enough observations to satisfy the `min_samples=30` threshold:

- `1990s` — 87 tracks
- `2000s` — 1,251 tracks
- `2010s` — 3,972 tracks

The first two principal components explain approximately **20% of the total variance**.

The genres overlap substantially in the PCA-2D representation.

This means that the visible clusters do not provide a clear separation between genres.

The `1990s` are particularly sparse and therefore difficult to interpret reliably.

---

## Elbow Analysis

The elbow method is used to investigate the appropriate number of clusters.

The inertia curves for all three decades are relatively smooth and do not show a strong elbow.

Therefore, the clustering structure is not strongly defined.

The results suggest that the audio-feature space behaves more like a relatively continuous distribution rather than clearly separated clusters.

---

# 2. Title & Genre Exploration

This section uses the textual metadata from `tracks.csv`.

Unlike the previous section, the analysis does not rely on the audio features.

The main variables are:

- Song titles
- Genres
- Release years

---

## 2.1 Genre Trend Over Time

The analysis investigates how the number and share of tracks belonging to different top genres change over time.

The available data mainly covers the period from `2008` to `2017`.

Most genres increase during the early 2010s and reach their highest levels around `2014–2016`.

There is a sharp decrease in `2017`.

However, this decline appears to be related to incomplete data for the final year rather than a genuine change in music popularity.

Therefore, this analysis should primarily be interpreted as a representation of **FMA catalogue growth**, rather than overall music popularity.

---

## 2.2 Vocabulary by Decade

The project analyses the most frequently used words in song titles across different decades.

The analysis shows that words such as:

- `You`
- `I`
- `Me`
- `Love`

are common across the catalogue.

One notable difference is the appearance of:

- `Remix`
- `Mix`

more prominently in the `2010s`.

This may reflect the increasing presence of remix-related tracks in the catalogue.

The word `Instrumental` is also highly frequent because many tracks are directly titled `Instrumental` or contain this word in their titles.

---

## 2.3 Title Duplication Over Time

The analysis measures the percentage of duplicated song titles within each decade.

Only the `2000s` and `2010s` contain enough observations for meaningful comparison.

The duplicate-title rate increases from approximately:

- `1.5%` in the `2000s`
- `2.6%` in the `2010s`

Possible explanations include:

- More tracks per artist
- More opportunities for title collisions
- Increased use of remix and cover titles
- Generic titles such as `Untitled` or `Intro`

The result therefore reflects both naming conventions and the growth of the FMA catalogue.

---

## 2.4 Genre Vocabulary Overlap

The vocabulary overlap between genres is measured using **Jaccard similarity**.

The Jaccard similarity is calculated as:

`intersection / union`

where the intersection represents words shared between two genres and the union represents all unique words appearing in both genres.

The off-diagonal similarity values are relatively small, approximately `0.08–0.18`.

This indicates that different genres generally have distinct title vocabularies.

### Main Observations

`Pop` and `Rock` have the highest vocabulary overlap at approximately `0.18`.

Other relatively high-overlap pairs include:

- `Folk` and `Rock` — `0.17`
- `Folk` and `Pop` — `0.16`

These genres therefore share more title vocabulary than the other analysed pairs.

`International` has the lowest overlap with most other genres, at approximately `0.08`.

`Hip-Hop` also shows relatively low overlap with other genres, with similarities around `0.13–0.15`.

Overall, the results suggest that title vocabulary is largely specific to individual genres, while `Pop`, `Rock`, and `Folk` show more vocabulary convergence.

---

# 3. Genre-Pair PCA Centroid Distances Over Time

This section investigates whether different music genres become more similar or more different in audio-feature space over time.

A global `PCA` is fitted using standardised audio features and cross-feature derivations.

The tracks are divided into five-year periods:

- `1980`
- `1985`
- `1990`
- `1995`
- `2000`
- `2005`
- `2010`

For each `(period, genre)` combination containing at least `10` tracks, a centroid is calculated in PCA-2D.

The Euclidean distance between two genre centroids is then calculated.

---

## Data Coverage

The release-date metadata in FMA is relatively sparse.

Approximately `57,000` of the `106,574` tracks do not have an `album.date_released` value.

As a result, many tracks cannot be assigned to a five-year period.

The available observations are also heavily concentrated after `2000`.

For the `small` subset, the number of non-null genre pairs is:

| Period | Non-null pairs |
|---|---:|
| `1980` | 0 |
| `1985` | 0 |
| `1990` | 0 |
| `1995` | 3 |
| `2000` | 15 |
| `2005` | 28 |
| `2010` | 28 |

Because of this data sparsity, the most reliable comparisons focus on the `2005–2010` period.

---

# 3.1 Distance Trends

The distance between two genre centroids represents their position relative to each other in the PCA-2D audio-feature space.

A decreasing distance indicates that the two genre centroids are becoming closer.

An increasing distance indicates that the two genre centroids are moving further apart.

Therefore:

- Falling distance → `converging`
- Rising distance → `diverging`
- Similar distance → `stable`

---

# 3.2 Interesting Genre Pairs

Genre pairs are considered interesting when their centroid distance changes by at least `30%` between the first and last available periods.

For the `small` subset:

`13 of 28 pairs` qualify as interesting.

For the `large` subset:

`65 of 120 pairs` qualify as interesting.

---

# 3.3 Key Findings

### Hip-Hop vs. Electronic

The centroid distance decreases from:

`0.84 → 0.25`

between `2005` and `2010`.

This represents a strong convergence in the PCA-2D representation.

### Electronic vs. Instrumental

The distance increases from:

`7.54 → 12.87`

between `2005` and `2010`.

This indicates divergence between the two genre centroids in PCA-2D.

### Electronic vs. Experimental

The distance increases from:

`5.27 → 8.76`

between `2005` and `2010`.

This also indicates divergence in the PCA representation.

### Electronic vs. International

The distance decreases from:

`7.43 → 5.78`.

This represents a moderate convergence.

### Electronic vs. Folk

The distance changes only slightly:

`12.44 → 12.39`.

This suggests a relatively stable relationship over the observed period.

---

# 4. Summary of Findings

## Section 1 — PCA + K-Means

The available data provides enough observations for three decades:

- `1990`
- `2000`
- `2010`

The PCA representation captures approximately `20%` of the total variance.

The genres overlap substantially in the two-dimensional representation.

The elbow curves are relatively smooth, suggesting that the audio-feature cloud does not contain strongly separated natural clusters.

---

## Section 2 — Title & Genre Exploration

The genre trends mainly reflect the changing composition and growth of the FMA catalogue.

The title vocabulary analysis shows that common words such as `You`, `I`, `Me`, and `Love` dominate song titles.

`Remix` and `Mix` become more prominent in the `2010s`.

The duplicate-title rate increases from approximately `1.5%` in the `2000s` to `2.6%` in the `2010s`.

Genre vocabulary overlap is generally low.

`Pop`, `Rock`, and `Folk` show relatively high vocabulary similarity, while `International` has relatively low overlap with the other genres.

---

## Section 3 — Genre-Pair PCA Distances

The genre-pair analysis uses a global PCA and measures the distance between genre centroids across five-year periods.

The analysis shows several examples of both convergence and divergence.

The strongest observed movement in the `small` subset is the convergence between `Hip-Hop` and `Electronic` between `2005` and `2010`.

However, the results should be interpreted carefully because the PCA representation only captures approximately `19–20%` of the total variance.

---

# Limitations

Several limitations should be considered when interpreting the results.

### 1. PCA is a Low-Dimensional Projection

The analysis uses only two PCA dimensions to calculate centroid distances.

The original dataset contains approximately `500` audio features.

Therefore, changes observed in PCA-2D may not necessarily represent equivalent changes in the full feature space.

---

### 2. Genre Composition Can Change

Changes in centroid distances can reflect two different effects:

- Actual stylistic changes in music
- Changes in which tracks are assigned to a particular genre

For example, if the composition of the `Folk` genre changes over time, the movement of its centroid may reflect changes in genre membership rather than changes in music style itself.

---

### 3. Short Time Series Are Noisy

Some genre pairs have observations for only two or three periods.

Large relative changes can therefore occur because of random variation.

Longer and more consistent trends provide stronger evidence than a single jump between two periods.

---

### 4. Sparse Pre-2000 Data

The FMA release-date metadata is concentrated heavily after `2000`.

Therefore, the analysis cannot provide a reliable picture of long-term genre evolution going back to the `1960s` or `1970s`.

The most reliable comparisons in this project focus on the `2005–2010` period.

---

# Future Improvements

Several extensions could improve the analysis.

## 1. Analyse the `large` Subset

Re-run the genre-pair analysis using:

`subset='large'`

This would allow analysis of:

- `16` genres
- `120` genre pairs

instead of:

- `8` genres
- `28` genre pairs

---

## 2. Use Full Feature-Space Distances

Instead of relying only on PCA-2D distances, future analysis could calculate distances directly in the standardised feature space.

Possible approaches include:

- `Euclidean distance`
- `Mahalanobis distance`

This would help determine whether movements observed in PCA-2D are projection artefacts.

---

## 3. Analyse Genre Membership Stability

Future analysis could examine how many tracks change their `genre_top` classification across different periods.

This would help distinguish between:

`stylistic drift`

and

`genre-tagging drift`.

---

# Technologies Used

- `Python`
- `Pandas`
- `NumPy`
- `Scikit-learn`
- `Matplotlib`
- `Seaborn`
- `librosa`
- `PCA`
- `K-Means`
- `Jaccard Similarity`
- `FMA Dataset`

---

# Project Structure

```text
FMA-Music-Dataset-Analysis/
│
├── data/
│   └── fma_metadata/
│
├── dataset.py
├── utils.py
├── visualization.py
├── visualizer.py
├── decade_analysis.py
├── genre_pair_analysis.py
│
├── notebook/
│
├── README.md
└── requirements.txt
