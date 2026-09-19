# Exploring-Music-Evolution

## About the Dataset

This project uses the **Free Music Archive (FMA)** dataset, a public dataset containing approximately **106,574 Creative Commons audio tracks** designed for music-information-retrieval research.

Each track includes metadata such as:

- Artist
- Album
- Track title
- Top-level genre
- Release date

In addition to the metadata, the dataset provides **518 pre-computed audio features** extracted using `librosa`, including MFCCs, chroma, spectral centroid, spectral bandwidth, spectral rolloff, spectral contrast, RMSE, zero-crossing rate (ZCR), and tonnetz features.

The FMA catalog is available in three main subsets:

- **FMA Small** – 8,000 tracks across 8 top-level genres
- **FMA Medium** – 25,000 tracks
- **FMA Large** – the full 106,574-track collection

The analyses in this project primarily use the **track metadata and pre-computed audio features** rather than the raw audio files.

## Overview

Music changes over time, but this evolution can be observed not only through sound, but also through the words artists choose and the ways different genres intersect.

Using the Free Music Archive (FMA) dataset, this project explores music evolution through a sequence of visualizations. We begin with the language of song titles, move to repeated titles and shared vocabulary between genres, and finally examine how genres move closer together or further apart in audio-feature space.


![Genre Trends Over Time](<Data image/Figure_1.png>)

---

## 1. How has the vocabulary of song titles changed?

The first visualization looks at the most frequent words appearing in song titles across decades.

![Vocabulary Evolution Across Decades](<Data image/Figure_2.png>)



## 2. How frequently do song titles overlap?


The duplication-rate visualization compares how frequently song titles are repeated within each decade.


![Song Title Duplication Rate](<Data image/Figure_3.png>)



## 3. How much vocabulary overlap exists between genres?


The heatmap measures the **Jaccard similarity** of title vocabularies between genres. Higher values indicate that two genres share a larger proportion of their unique title words.

![Genre Vocabulary Overlap](<Data image/Figure_4.png>)



## 4. Do songs and genres move closer together stylistically?

Genres are represented by their centroids in a two-dimensional PCA space. The distance between two genre centroids provides a visual measure of how close or far apart their audio characteristics are over time.

A **falling line** indicates convergence, while a **rising line** indicates divergence.

![Genre Pair Distance Trends]<img width="2020" height="778" alt="Figure_5" src="https://github.com/user-attachments/assets/5aa56ec4-7bcf-4b26-8378-3369e386da78" />



## 5. Seeing stylistic movement directly

The time-strip visualization provides another perspective by showing the actual genre clouds and their centroids across five-year periods.

Rather than looking only at numerical distances, we can visually follow how the two genre distributions move through PCA space.

![Genre Pair Time Strip](path/to/pair_time_strip.png)





