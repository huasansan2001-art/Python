# Overview
FMA Music Dataset analysis
About the dataset
The Free Music Archive (FMA) is a public dataset of ~106 574 Creative- Commons audio tracks released by Defferrard et al. (2017), built to support music-information-retrieval research. Each track ships with metadata (artist, album, title, top-level genre, release date) and 518 pre-computed audio features extracted via librosa (MFCC, chroma, spectral centroid / bandwidth / rolloff / contrast, RMSE, ZCR, tonnetz). The catalog is organised into three nested subsets — (8 000 tracks, balanced across 8 top
genres),
of tracks with no
subset (
metadata + features archives, which dataset.py downloads automatically in the next cell.
medium
small
(25 000), and (the full 106 574) — plus a long-tail label. The audio itself is available as MP3s per
large
set.subset
fma_small
is ~7 GB); the analyses in this notebook only need the
What we are analysing
Section 1 — Per-decade PCA + k-means. For each decade with enough tracks, we project the FMA audio-feature space to 2D via PCA and overlay k- means clusters (k chosen by elbow detection). The goal is to see how the geometry of the audio-feature space differs across decades.
Section 2 — Title & genre exploration. Four lexical / metadata views over the catalog:
2.1 how the share of each top genre evolves over time,
2.2 the most frequent words in song titles per decade (word clouds),
2.3 how often song titles repeat within a decade,
2.4 pairwise vocabulary overlap between top genres (Jaccard similarity).
Section 3 — Genre-pair PCA centroid distances over 5y periods. We fit one global PCA on standardized audio features, then for each 5y period compute the centroid of each top genre in PCA-2D. For every genre pair we measure the Euclidean distance between their centroids per period and track how that distance moves over time. The question: do genre pairs converge or diverge in audio-feature space as time progresses?
