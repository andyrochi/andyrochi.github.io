---
title: "Spotify Tracks Dataset Visualization"
date: 2022-12-05
draft: false
tags: ["data-visualization"]
technologies: ["javascript", "d3.js"]
weight: 3
summary: "Spotify Tracks DataVis is an interactive web tool for exploring trends and insights from over 160,000 Spotify tracks. Built with JavaScript and D3.js, it visualizes attributes like genre, popularity, and audio features using bar charts, radar plots, histograms, and more."
---

{{< button href="https://andyrochi.github.io/spotify-tracks-datavis" target="_blank" >}}
Spotify Tracks DataVis
{{< /button >}}
{{< button href="https://github.com/andyrochi/spotify-tracks-datavis" target="_blank" >}}
{{< icon "github" >}}
{{< /button >}}

Spotify Tracks DataVis is an interactive web tool for exploring trends and insights from over 160,000 Spotify tracks. Built with JavaScript and D3.js, it visualizes attributes like genre, popularity, and audio features using bar charts, radar plots, histograms, and more.

This is a simple data visualization project that explores the [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset?resource=download) from Kaggle.

The project was built using vanilla JavaScript, D3.js, and Bootstrap.

## System Introduction

{{<figure src="https://user-images.githubusercontent.com/39425103/203897825-34c95da3-b6c7-4020-97df-6c36ce9d16ba.png" alt="" width="100%">}}

The figure above shows a preview of the entire system. We introduce each section below.

## A. Filtering

Clicking on the **Filter** button in the upper-right corner reveals a sidebar where various modifications to the dataset can be made.

<img src="https://user-images.githubusercontent.com/39425103/203897906-70a91d66-41ab-4e2b-a775-0fbd63a06ee0.png" alt="sidebar" style="max-width: 100%;">

### 1. Selecting interested genres

Use the dropdown to select genres you’re interested in visualizing and comparing.

<img src="https://user-images.githubusercontent.com/39425103/203897918-4f1fc6e1-bc73-4c4f-a389-2c835ee610be.png" alt="genre-selection" style="max-width: 100%;">

### 2. Sorting the data

You can sort the data by any numerical attribute and choose either ascending or descending order.

<img src="https://user-images.githubusercontent.com/39425103/203897926-ba625cd8-dbfb-467b-abaa-3c7deddeeb53.png" alt="data-sorting" style="max-width: 100%;">

### 3. Selecting the TOP N% rows of each genre

To perform deeper analysis, adjust the slider to choose how much of the dataset you want to include.

<img src="https://user-images.githubusercontent.com/39425103/203897932-a01ee504-d588-453c-baec-6a9fcaaacb72.png" alt="data-selection" style="max-width: 100%;">

Here, we selected the **top 30%** of tracks by **popularity** within each genre.

Modifying the filters helps reveal several insights about the data.

## B. Single Genre Analysis

This section allows you to examine the properties of one genre at a time.

<img src="https://user-images.githubusercontent.com/39425103/203897950-1ab0e5f5-3a1a-4b97-a89f-1224b6778383.png" alt="genre-selection" style="max-width: 100%;">

Select the genre from the dropdown:

<img src="https://user-images.githubusercontent.com/39425103/203897972-735f1bcc-c771-4d91-b1f4-384a38be7ca8.png" alt="genre-dropdown" style="max-width: 100%;">

Different views will be shown:

<img src="https://user-images.githubusercontent.com/39425103/203897983-841ac79d-6cb1-4d1a-bd60-cb1065672077.png" alt="views" style="max-width: 100%;">

### 1. Histogram of Numerical Attributes

Histograms show the distribution of numerical features within a genre.

For example, classical music tends to have high **acousticness**:

<img src="https://user-images.githubusercontent.com/39425103/203897992-d2a5f458-4f29-447d-8e37-a8bd3bb58fff.png" alt="acousticness" style="max-width: 100%;">

But not much **energy**:

<img src="https://user-images.githubusercontent.com/39425103/203898475-d42384bc-ae63-4307-a775-8a73b98564bf.png" alt="no-energy" style="max-width: 100%;">

### 2. Count of Each Key and Mode

<img src="https://user-images.githubusercontent.com/39425103/203898487-b67ceff9-654b-4ce6-b84a-134e7cb32f7f.png" alt="key-mode" style="max-width: 100%;">

We can see that many popular classical tracks are written in **major** keys, especially those with sharps. **D major** is the most common, which aligns with the idea that it sounds heavenly or divine in Western music theory.

### 3. Pie Chart of Explicit Lyrics

For single genres, we show the number of tracks with explicit lyrics. For the **all-genres** category, we show a different chart explained later.

<img src="https://user-images.githubusercontent.com/39425103/203898505-296c3701-8888-4969-adab-e1ae7e2cc231.png" alt="pie-chart" style="max-width: 100%;">

Classical music contains no explicit lyrics.

Some genres like j-rock contain a few:

<img src="https://user-images.githubusercontent.com/39425103/203898518-2461c5ba-1475-43aa-a8ca-70763418f5ce.png" alt="j-rock" style="max-width: 100%;">

## C. Cross-Genre Analysis and Visualization

### 1. Violin Plot for Numerical Distribution

I was curious about how different features vary across genres, so I created violin plots.

Here’s one for **valence**:

<img src="https://user-images.githubusercontent.com/39425103/203898531-779f0009-b13a-4cd3-93d8-b42236142249.png" alt="" style="max-width: 100%;">

**Valence** measures how positive a track sounds (0.0 = sad, 1.0 = happy).  
Mandopop tends to have lower valence—many Taiwanese and Chinese songs are more melancholic. Japanese songs generally have higher valence.

### 2. Radar Plot for Averaged Statistics

<img src="https://user-images.githubusercontent.com/39425103/203898554-1d51a550-54f8-48d5-ab94-65c8c3a8a798.png" alt="radar-plot" style="max-width: 100%;">

The radar plot shows how genres differ in average attributes.  
Classical music is high in acousticness, Japanese music is high in energy, and most selected genres have decent danceability.

### 3. Top 20 Genres in “All-Genres” Mode

This chart is shown when analyzing **all genres** together.

<img src="https://user-images.githubusercontent.com/39425103/203898572-e2449351-8c32-4583-8c33-d664a0c0c4bb.png" alt="all-genre" style="max-width: 100%;">

With the top 30% most popular tracks selected, the most common genres are pop-film, chill, and k-pop.

If we change the filter to show the top 1% tracks with the highest **valence**:

<img src="https://user-images.githubusercontent.com/39425103/203898584-20a7d745-c069-4350-825e-3d17c596a8fb.png" alt="filter" style="max-width: 100%;">

We get:

<img src="https://user-images.githubusercontent.com/39425103/203898651-90211eeb-a52e-44b7-9fff-ee6ff33323e0.png" alt="valence" style="max-width: 100%;">

Children’s music ranks highest in positivity, and cheerful music tends to have more energy (top-left quadrant).

---

Feel free to explore the tool and uncover your own insights!