# Exploring-Music-Evolution

## Overview

Music changes over time, but this evolution can be observed not only through sound, but also through the words artists choose and the ways different genres intersect.

Using the Free Music Archive (FMA) dataset, this project explores music evolution through a sequence of visualizations. We begin with the language of song titles, move to repeated titles and shared vocabulary between genres, and finally examine how genres move closer together or further apart in audio-feature space.

The analysis is guided by four questions:

1. How has the vocabulary used in song titles changed across different decades?
2. How frequently do song titles overlap within a specific dataset?
3. How much overlap exists between song titles of different genres?
4. How do songs influence one another stylistically or lyrically?

---

## 1. How has the vocabulary of song titles changed?

The first visualization looks at the most frequent words appearing in song titles across decades.

### Vocabulary Evolution Across Decades

The word clouds show a strong continuity in the language used in song titles. Words such as **"You"**, **"I"**, **"Me"**, and **"Love"** dominate both periods, suggesting that personal pronouns and emotional themes remain common throughout the catalog.

At the same time, the 2010s introduce a more visible presence of words such as **"Remix"** and **"Mix"**, which are much less prominent in the 2000s. This provides a visual indication of changing naming conventions and the growing presence of remix-oriented releases.

The word **"Instrumental"** is also highly visible in both decades, partly because a large number of tracks use it directly in their titles.

![Vocabulary Evolution Across Decades](path/to/vocabulary_evolution.png)

**What the visualization tells us:**  
Song-title vocabulary shows both continuity and change. Core emotional and personal vocabulary remains persistent, while terms associated with newer production and release practices become more visible over time.

---

## 2. How frequently do song titles overlap?

After looking at individual words, the next question is whether artists also reuse complete song titles.

### Song Title Duplication Rate Across Decades

The duplication-rate visualization compares how frequently song titles are repeated within each decade.

The rate increases from approximately **1.5% in the 2000s to 2.6% in the 2010s**. This means that title collisions become more common in the later period.

Several factors may contribute to this pattern, including a larger number of tracks, repeated use of generic titles such as **"Untitled"** or **"Intro"**, and the growing presence of remix and cover releases.

![Song Title Duplication Rate](path/to/title_duplication.png)

**What the visualization tells us:**  
As the catalog becomes denser, repeated song titles become more frequent. Title reuse therefore provides another dimension of change beyond the vocabulary itself.

---

## 3. How much vocabulary overlap exists between genres?

The next step is to move from individual decades to relationships between genres.

### Genre Vocabulary Overlap

The heatmap measures the **Jaccard similarity** of title vocabularies between genres. Higher values indicate that two genres share a larger proportion of their unique title words.

The visualization shows that most genre pairs have relatively low overlap, with off-diagonal similarities ranging from roughly **0.08 to 0.18**.

The strongest overlap appears among:

- **Pop & Rock: 0.18**
- **Folk & Rock: 0.17**
- **Folk & Pop: 0.16**

These genres therefore share more title vocabulary with one another than with most other genres.

In contrast, **International** has very low overlap with the other genres, around **0.08–0.09**, while **Hip-Hop** also shows relatively distinct vocabulary.

![Genre Vocabulary Overlap](path/to/genre_overlap_heatmap.png)

**What the visualization tells us:**  
Genres are not completely isolated linguistically, but their title vocabularies remain largely distinct. The strongest overlap appears among genres that are relatively close within the popular-music landscape.

---

## 4. Do songs and genres move closer together stylistically?

Shared words are only one side of musical similarity. Two genres may use different language while becoming more similar in sound.

To explore this, the final visualizations move from text to **audio-feature space**.

### Genre-Pair Distance Trends

Genres are represented by their centroids in a two-dimensional PCA space. The distance between two genre centroids provides a visual measure of how close or far apart their audio characteristics are over time.

A **falling line** indicates convergence, while a **rising line** indicates divergence.

![Genre Pair Distance Trends](path/to/pair_distance_trends.png)

Several patterns stand out in the later periods:

- **Hip-Hop and Electronic** move substantially closer together, with their centroid distance decreasing from **0.84 to 0.25** between 2005 and 2010.
- **Electronic and Instrumental** move further apart, from **7.54 to 12.87**.
- **Electronic and Experimental** also diverge, from **5.27 to 8.76**.
- **Electronic and International** show mild convergence, from **7.43 to 5.78**.
- **Electronic and Folk** remain relatively stable, changing only from **12.44 to 12.39**.

These movements suggest that musical styles do not evolve in a single direction. Some genre pairs become more similar, while others become more distinct.

---

## 5. Seeing stylistic movement directly

The time-strip visualization provides another perspective by showing the actual genre clouds and their centroids across five-year periods.

Rather than looking only at numerical distances, we can visually follow how the two genre distributions move through PCA space.

![Genre Pair Time Strip](path/to/pair_time_strip.png)

This visualization makes the idea of **convergence and divergence** more intuitive:

- when two genre clouds move toward one another, their styles become more similar in the projected feature space;
- when they move apart, their styles become more distinct.

The visualization therefore complements the title-based analysis: linguistic overlap tells us **what genres have in common in their titles**, while PCA distance tells us **how their sound-space positions change over time**.

---

## 6. From words to sound: the overall story

The visualizations reveal a layered picture of music evolution.

Song titles show substantial continuity: words related to personal experience and emotion remain common across decades. At the same time, new terminology such as **"Remix"** becomes more prominent, indicating changes in naming conventions.

Complete title duplication also becomes more frequent, rising from about **1.5% to 2.6%** between the 2000s and 2010s. This suggests that the growing catalog contains more repeated or generic naming patterns.

Across genres, however, title vocabularies remain mostly distinct. The strongest lexical connections appear among **Pop, Rock, and Folk**, while genres such as **International** and **Hip-Hop** show more distinct vocabulary profiles.

Finally, the audio visualizations show that stylistic relationships are dynamic. Some genre pairs converge while others diverge, meaning that musical evolution is not simply a process of all genres becoming more alike.

Together, the visualizations tell a story of **continuity, repetition, lexical separation, and selective stylistic convergence**.

---

## Visualizations

The project focuses on the following visual analyses:

1. **Vocabulary Evolution Across Decades**  
   Word clouds showing the most frequent words in song titles.

2. **Song Title Duplication Rate**  
   Line chart showing the share of repeated song titles across decades.

3. **Genre Vocabulary Overlap**  
   Jaccard-similarity heatmap showing shared title vocabulary between genres.

4. **Genre-Pair Distance Trends**  
   Small multiples showing how genre distances change over time in PCA space.

5. **Genre-Pair Time Strip**  
   Visual comparison of genre distributions and centroids across five-year periods.

---

## Key Takeaway

Music evolution can be seen from several complementary perspectives. The words in song titles retain strong recurring themes, titles are reused more frequently in later periods, genres maintain mostly distinct vocabularies, and their musical characteristics can either converge or diverge over time.

Rather than showing one universal direction of musical change, the visualizations reveal a more nuanced process in which **some elements remain stable while others evolve and interact differently across genres**.
