# FMA Music Dataset Analysis

This repository contains the analysis of the **Free Music Archive (FMA)** dataset using audio features and textual metadata.

The project investigates the structure of music across different decades, explores song title vocabulary and genre trends, and analyses how different music genres converge or diverge in audio-feature space over time.

---

## 📌 Table of Contents

1. [📦 Project Structure](#-project-structure)
2. [📋 Project Description](#-project-description)
   - [1. About Dataset](#1-about-dataset)
   - [2. Dataset Preparation](#2-dataset-preparation)
   - [3. Per-Decade PCA + K-Means](#3-per-decade-pca--k-means)
   - [4. Title & Genre Exploration](#4-title--genre-exploration)
   - [5. Genre-Pair PCA Centroid Distances](#5-genre-pair-pca-centroid-distances)
   - [6. Summary of Findings](#6-summary-of-findings)
   - [7. Limitations](#7-limitations)
   - [8. Future Improvements](#8-future-improvements)
3. [⚙️ Technologies Used](#%EF%B8%8F-technologies-used)
4. [🚀 Usage](#-usage)
5. [📚 References](#-references)

---

## 📦 Project Structure

The repository is organized into the following directories and files:

- **/data**: Contains the FMA dataset and metadata.
- **/notebook**: Contains the Jupyter Notebook used for the analysis.
- **dataset.py**: Handles downloading and preparing the FMA dataset.
- **utils.py**: Provides utility functions for loading and processing data.
- **visualization.py**: Contains functions for metadata and genre visualizations.
- **visualizer.py**: Contains visualization functions for PCA, clustering, and genre-pair analysis.
- **decade_analysis.py**: Performs the per-decade PCA and K-Means analysis.
- **genre_pair_analysis.py**: Performs genre-pair centroid distance analysis.
- **README.md**: Project documentation.
- **requirements.txt**: Required Python packages.

---

# 📋 Project Description

## 1. About Dataset

The **Free Music Archive (FMA)** is a public dataset containing approximately **106,574 Creative Commons audio tracks**.

The dataset was released by Defferrard et al. (2017) and was designed to support research in **music information retrieval**.

Each track contains metadata such as:

- Artist
- Album
- Track title
- Top-level genre
- Release date

The dataset also provides **518 pre-computed audio features**, including:

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

| Subset | Number of Tracks |
|---|---:|
| `small` | 8,000 |
| `medium` | 25,000 |
| `large` | 106,574 |

The analysis in this project primarily uses the **metadata and pre-computed audio features** rather than the raw audio files. :contentReference[oaicite:1]{index=1}

---

## 2. Dataset Preparation

The project uses two main metadata files:

- `tracks.csv`
- `features.csv`

The dataset contains:

- `106,574` tracks
- `52` metadata columns
- `518` audio-feature columns

The dataset is downloaded and extracted into the `data/` directory before running the analysis. :contentReference[oaicite:2]{index=2}

---

## 3. Per-Decade PCA + K-Means

The first part of the project investigates the structure of the audio-feature space across different decades.

### 3.1 Principal Component Analysis

`PCA` is used to reduce the high-dimensional audio-feature space to two dimensions.

The analysis is performed on standardised audio features together with cross-feature derivations.

The two-dimensional representation allows the audio-feature space to be visualised and compared across different decades.

### 3.2 K-Means Clustering

`K-Means` clustering is applied to the PCA representation.

The number of clusters is investigated using the **elbow method** and `KneeLocator`.

Only decades containing at least `30` tracks are included in the analysis.

The analysed decades are:

| Decade | Number of Tracks |
|---|---:|
| `1990s` | 87 |
| `2000s` | 1,251 |
| `2010s` | 3,972 |

### 3.3 Results

The first two principal components explain approximately **20% of the total variance**.

The genres overlap substantially in the PCA-2D representation.

The elbow curves are relatively smooth and do not show a strong natural clustering structure.

As a result, the audio-feature space appears to behave more like a relatively continuous distribution rather than clearly separated clusters.

---

## 4. Title & Genre Exploration

The second part of the project focuses on textual and metadata information from `tracks.csv`.

This section does not use the audio features.

The analysis consists of four parts:

1. Genre trend over time
2. Vocabulary by decade
3. Title duplication over time
4. Genre vocabulary overlap

---

### 4.1 Genre Trend Over Time

This analysis investigates how the number of tracks belonging to different top genres changes over time.

The available data mainly covers the period from **2008 to 2017**.

Most genres increase during the early 2010s and reach their highest levels around `2014–2016`.

The sharp decline in `2017` is likely related to incomplete data for the final year.

Therefore, the result should primarily be interpreted as a representation of **FMA catalogue growth**, rather than overall music popularity. :contentReference[oaicite:3]{index=3}

---

### 4.2 Vocabulary by Decade

This analysis investigates how the vocabulary used in song titles changes across decades.

The most frequent words include:

- `You`
- `I`
- `Me`
- `Love`

These words are common across the analysed catalogue.

One notable difference is that:

- `Remix`
- `Mix`

appear more prominently in the `2010s` than in the `2000s`.

The word `Instrumental` is also highly frequent because many tracks contain this word directly in their titles. :contentReference[oaicite:4]{index=4}

---

### 4.3 Title Duplication Over Time

This analysis measures how frequently song titles are duplicated within each decade.

Only the `2000s` and `2010s` contain enough observations for comparison.

| Decade | Duplicate Title Rate |
|---|---:|
| `2000s` | 1.5% |
| `2010s` | 2.6% |

The duplicate-title rate therefore increases from approximately **1.5% to 2.6%**.

Possible explanations include:

- More tracks per artist
- More opportunities for title collisions
- Increased use of remix and cover titles
- Generic titles such as `Untitled` or `Intro` :contentReference[oaicite:5]{index=5}

---

### 4.4 Genre Vocabulary Overlap

The vocabulary overlap between genres is measured using **Jaccard similarity**.

Jaccard similarity is calculated as:

`intersection / union`

The results show relatively low vocabulary overlap between most genres.

The observed off-diagonal similarities range approximately from `0.08` to `0.18`.

The highest-overlap genre pairs are:

| Genre Pair | Jaccard Similarity |
|---|---:|
| `Pop` – `Rock` | 0.18 |
| `Folk` – `Rock` | 0.17 |
| `Folk` – `Pop` | 0.16 |

`International` has relatively low vocabulary overlap with the other analysed genres, at approximately `0.08`.

Overall, the results suggest that song-title vocabularies are largely distinct between genres, while `Pop`, `Rock`, and `Folk` show greater vocabulary similarity. :contentReference[oaicite:6]{index=6}

---

# 5. Genre-Pair PCA Centroid Distances

The third part of the project investigates whether different genres become more similar or more different in audio-feature space over time.

A global `PCA` is fitted using standardised audio features and cross-feature derivations.

Tracks are then divided into five-year periods:

- `1980`
- `1985`
- `1990`
- `1995`
- `2000`
- `2005`
- `2010`

For every `(period, genre)` combination containing at least `10` tracks, a centroid is calculated in PCA-2D.

The **Euclidean distance** between genre centroids is then calculated for each period.

The main research question is:

> **Are genre pairs converging or diverging over time?**

:contentReference[oaicite:7]{index=7}

---

## 5.1 Data Coverage

The release-date metadata in FMA is relatively sparse.

Approximately `57,000` of the `106,574` tracks do not have an `album.date_released` value.

As a result, many tracks cannot be assigned to a five-year period.

The available release-date observations are also heavily concentrated after `2000`.

For the `small` subset:

| Period | Non-null Genre Pairs |
|---|---:|
| `1980` | 0 |
| `1985` | 0 |
| `1990` | 0 |
| `1995` | 3 |
| `2000` | 15 |
| `2005` | 28 |
| `2010` | 28 |

Therefore, the most reliable comparisons focus on the `2005–2010` period. :contentReference[oaicite:8]{index=8}

---

## 5.2 Distance Trends

The distance between two genre centroids represents their relative position in PCA-2D.

- **Decreasing distance** → `converging`
- **Increasing distance** → `diverging`
- **Similar distance** → `stable`

This allows the project to identify genre pairs whose audio-feature representations change substantially over time.

---

## 5.3 Interesting Genre Pairs

A genre pair is classified as interesting when its centroid distance changes by at least **30%** between the first and last available periods.

For the `small` subset:

`13 of 28 pairs` qualify as interesting.

For the `large` subset:

`65 of 120 pairs` qualify as interesting. :contentReference[oaicite:9]{index=9} :contentReference[oaicite:10]{index=10}

---

## 5.4 Key Findings

### Hip-Hop vs. Electronic

The centroid distance decreases from:

`0.84 → 0.25`

between `2005` and `2010`.

This represents a strong convergence in the PCA-2D representation.

### Electronic vs. Instrumental

The centroid distance increases from:

`7.54 → 12.87`

between `2005` and `2010`.

This represents divergence in PCA-2D.

### Electronic vs. Experimental

The centroid distance increases from:

`5.27 → 8.76`

between `2005` and `2010`.

This also represents divergence.

### Electronic vs. International

The centroid distance decreases from:

`7.43 → 5.78`

indicating moderate convergence.

### Electronic vs. Folk

The distance changes only slightly:

`12.44 → 12.39`

indicating a relatively stable relationship.

These results are based on the actual centroid-distance matrix from the analysis. :contentReference[oaicite:11]{index=11}

---

# 6. Summary of Findings

## Section 1 — PCA + K-Means

The available data provides enough observations for three decades:

- `1990`
- `2000`
- `2010`

The first two PCA components explain approximately `20%` of the variance.

The genres overlap substantially in the two-dimensional representation.

The elbow curves are relatively smooth, suggesting that there is no strongly separated natural cluster structure in the analysed PCA representation.

---

## Section 2 — Title & Genre Exploration

The genre trends mainly reflect changes in the composition and growth of the FMA catalogue.

The title vocabulary analysis shows that common words such as `You`, `I`, `Me`, and `Love` dominate song titles.

`Remix` and `Mix` become more prominent in the `2010s`.

The duplicate-title rate increases from approximately `1.5%` in the `2000s` to `2.6%` in the `2010s`.

Genre vocabulary overlap is generally low, with relatively higher similarity between `Pop`, `Rock`, and `Folk`. :contentReference[oaicite:12]{index=12}

---

## Section 3 — Genre-Pair PCA Distances

The genre-pair analysis identifies examples of both convergence and divergence in PCA-2D.

The strongest observed movement in the `small` subset is the convergence between `Hip-Hop` and `Electronic` between `2005` and `2010`.

However, these results should be interpreted carefully because PCA-2D represents only approximately `19–20%` of the total variance. :contentReference[oaicite:13]{index=13}

---

# 7. Limitations

## 7.1 PCA-2D Projection

The original dataset contains approximately `500` audio features, while the centroid analysis uses only two PCA dimensions.

Therefore, a movement observed in PCA-2D may not necessarily represent the same movement in the full feature space.

---

## 7.2 Genre Composition

Changes in centroid distances can reflect both:

- Actual stylistic changes
- Changes in the composition of tracks assigned to a genre

Therefore, centroid movement should not automatically be interpreted as pure stylistic evolution.

---

## 7.3 Short Time Series

Some genre pairs contain only two or three available periods.

Large relative changes can therefore occur because of random variation.

Longer and more consistent trends provide stronger evidence than a single jump between two periods.

---

## 7.4 Sparse Pre-2000 Data

The release-date metadata is heavily concentrated after `2000`.

Therefore, the project cannot provide a reliable long-term analysis extending back to the `1960s` or `1970s`.

The most reliable comparisons focus on the `2005–2010` period. :contentReference[oaicite:14]{index=14}

---

# 8. Future Improvements

Several improvements could extend the analysis.

### 8.1 Analyse the Large Subset

Re-run the genre-pair analysis using the `large` subset.

This would increase the analysis from:

- `8` genres and `28` pairs

to:

- `16` genres and `120` pairs.

### 8.2 Use Full Feature-Space Distances

Calculate distances directly in the standardised feature space instead of relying only on PCA-2D.

Possible approaches include:

- `Euclidean distance`
- `Mahalanobis distance`

This could help determine whether observed movements are caused by the PCA projection.

### 8.3 Analyse Genre Membership Stability

Analyse how many tracks change their `genre_top` classification across different periods.

This could help distinguish between:

- `Stylistic drift`
- `Genre-tagging drift`

These extensions are also identified as reasonable next steps in the original analysis. :contentReference[oaicite:15]{index=15}

---

# ⚙️ Technologies Used

The project was developed using:

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
- `Euclidean Distance`

---

# 🚀 Usage

This project is designed to be completed in the following steps:

1. **Download the Repository**: Clone or download this repository to your local machine.

2. **Install the Requirements**: Install all required Python packages listed in `requirements.txt`.

3. **Prepare the Dataset**: Download the FMA dataset and place the required metadata files inside the `data/` directory.

4. **Run the Notebook**: Open the project notebook in Jupyter Notebook or JupyterLab.

5. **Run the Analysis**:
   - Per-decade PCA + K-Means
   - Genre trend analysis
   - Song-title vocabulary analysis
   - Title duplication analysis
   - Genre vocabulary overlap
   - Genre-pair PCA centroid distances

6. **Explore the Results**: Review the generated visualisations and tables to investigate patterns in the FMA dataset.

---

# 📚 References

- Defferrard, M., Benzi, K., Vandergheynst, P., & Bresson, X. (2017). **FMA: A Dataset for Music Analysis**.

- Free Music Archive: **FMA Dataset**

- Scikit-learn documentation: **Principal Component Analysis (PCA)**

- Scikit-learn documentation: **K-Means Clustering**

- Jaccard Similarity: **Set-based similarity measure**
