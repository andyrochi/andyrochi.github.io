---
title: "Spotify Tracks Dataset Visualization"
date: 2022-12-05
draft: false
project_tags: ["data-visualization", "javascript", "d3.js"]
status: "evergreen"
weight: 2
summary: "Visualizing the spotify tracks dataset"
links:
    external_link:
        text: "project link"
        icon: "fas fa-external-link-alt"
        href: "https://andyrochi.github.io/spotify-tracks-datavis"
        weight: 1
    another_link:
        text: "github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/andyrochi/spotify-tracks-datavis"
        weight: 2
---
# Spotify Tracks Dataset Visualization

This is a simple data visualization project that visualizes the [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset?resource=download) from Kaggle.

The demo of the website can be viewed [here](https://andyrochi.github.io/spotify-tracks-datavis/).

This project is created using vanilla javascript, D3.js, and Bootstrap.

# System Introduction

{{<figure src="https://user-images.githubusercontent.com/39425103/203897825-34c95da3-b6c7-4020-97df-6c36ce9d16ba.png" alt="" width="100%">}}


The figure here shows a preview of the entire system.

We introduce them section by section.

## A. Filtering

By clicking on the **Filter** button on the upper right corner, it shows a sidebar where we can perform various modifications to the dataset.

<img src="https://user-images.githubusercontent.com/39425103/203897906-70a91d66-41ab-4e2b-a775-0fbd63a06ee0.png" alt="sidebar" style="max-width: 100%;">


### 1. Selecting interested genres

By clicking on the dropdown, we can select genres that we are interested in to visualize and compare.

<img src="https://user-images.githubusercontent.com/39425103/203897918-4f1fc6e1-bc73-4c4f-a389-2c835ee610be.png" alt="genre-selection" style="max-width: 100%;">

### 2. Sorting the data

Then, we can choose to sort the data according to any of the numerical attributes and decide the ascending or descending order.

<img src="https://user-images.githubusercontent.com/39425103/203897926-ba625cd8-dbfb-467b-abaa-3c7deddeeb53.png" alt="data-sorting" style="max-width: 100%;">

### 3. Selecting the TOP N% rows of each genre

In order to perform in-depth analysis, we can drag the bar below to decide how much data do we want to view.

<img src="https://user-images.githubusercontent.com/39425103/203897932-a01ee504-d588-453c-baec-6a9fcaaacb72.png" alt="data-selection" style="max-width: 100%;">

We have selected the **top 30%** tracks according to **popularity** (the top 30% popular) of each genre.

By modifying the filter, we can gain several insights about the data.



## B. Single Genre Analysis

In this section, we can choose to observe the properties of a single genre.


<img src="https://user-images.githubusercontent.com/39425103/203897950-1ab0e5f5-3a1a-4b97-a89f-1224b6778383.png" alt="genre-selection" style="max-width: 100%;">

By selecting the genre in the dropdown:

<img src="https://user-images.githubusercontent.com/39425103/203897972-735f1bcc-c771-4d91-b1f4-384a38be7ca8.png" alt="genre-dropdown" style="max-width: 100%;">

different views will be shown:

<img src="https://user-images.githubusercontent.com/39425103/203897983-841ac79d-6cb1-4d1a-bd60-cb1065672077.png" alt="views" style="max-width: 100%;">

### 1. Histogram of Numerical Attributes

The histogram serves as a tool to see the different distributions of a certain feature with respect to a genre.

For example, we can see that the classical music genre has high **acousticness**.

<img src="https://user-images.githubusercontent.com/39425103/203897992-d2a5f458-4f29-447d-8e37-a8bd3bb58fff.png" alt="acousticness" style="max-width: 100%;">


However, it does not have high **energy**.

<img src="https://user-images.githubusercontent.com/39425103/203898475-d42384bc-ae63-4307-a775-8a73b98564bf.png" alt="no-energy" style="max-width: 100%;">


### 2. Count of each key and mode

<img src="https://user-images.githubusercontent.com/39425103/203898487-b67ceff9-654b-4ce6-b84a-134e7cb32f7f.png" alt="key-mode" style="max-width: 100%;">

We can see that a large portion of popular classical music is composed in **major** scales, and scales with sharps # (升記號) are quite common too. D major is the most popular in classical music, which matches my perception, since it is common explained that **D major** sounds like the music from heaven (in the west), which makes us closer to god.



### 3. Pie chart showing the number of songs with explicit lyrics

For "single" genres, we show the pie chart of the number of song that include explicit lyrics. for the **all-genres** category, we show a separate chart that we will explain later.

<img src="https://user-images.githubusercontent.com/39425103/203898505-296c3701-8888-4969-adab-e1ae7e2cc231.png" alt="pie-chart" style="max-width: 100%;">

There are no songs with explicit lyrics in the classical music genre.

Where j-rock consists of some.

<img src="https://user-images.githubusercontent.com/39425103/203898518-2461c5ba-1475-43aa-a8ca-70763418f5ce.png" alt="j-rock" style="max-width: 100%;">



## C. Cross Genre Analysis and Visualization

### 1. Violin Plot for Numerical Distribution Analysis 

I am interested in the distribution of different feature and attributes among genres, thus I created a violin chart to do so.

We can see that **valence** is an interesting feature to observe:

<img src="https://user-images.githubusercontent.com/39425103/203898531-779f0009-b13a-4cd3-93d8-b42236142249.png" alt="" style="max-width: 100%;">


**valence**: A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more negative (e.g. sad, depressed, angry).

We can see that **popular** mandopop (國語流行音樂) has a relatively lower valence, which shows that the Taiwanese and Chinese typically like to write sad music more. And for the Japanese, their distribution is much higher.

### 2. Radar Plot for Averaged Statistics

<img src="https://user-images.githubusercontent.com/39425103/203898554-1d51a550-54f8-48d5-ab94-65c8c3a8a798.png" alt="radar-plot" style="max-width: 100%;">

For the genres that I have selected, we can see that they differ quite a lot in the radar plot. Classical music feature the most acousticness, while japanese music mostly have a lot of energy. The common part among all is that most of the tracks selected have a quite danceability.

### 3. Top 20 genres in the selected portion of "all-genres"

This plot is only available if we chose "all-genres" to analyze individually.

<img src="https://user-images.githubusercontent.com/39425103/203898572-e2449351-8c32-4583-8c33-d664a0c0c4bb.png" alt="all-genre" style="max-width: 100%;">


Since we have selected the top 30% popular tracks, and we have chose to visualize **all genres**, we can actually count the number of each genre in the selection, and list the top 20 genres that made it into the list.

In this plot, we can see that the tracks that made into the top 30% list come from pop-film, chill, and k-pop.

If we changed the filter a bit, which is as follows:

<img src="https://user-images.githubusercontent.com/39425103/203898584-20a7d745-c069-4350-825e-3d17c596a8fb.png" alt="filter" style="max-width: 100%;">

We select the top 1% of tracks that has the most **valence** (most cheerful and happy), the results are quite interesting.

<img src="https://user-images.githubusercontent.com/39425103/203898651-90211eeb-a52e-44b7-9fff-ee6ff33323e0.png" alt="valence" style="max-width: 100%;">

We can see that children music are the ones that are the most happy. And for all genres, music that are cheerful (with high valence) usually has higher energy (top left corner).

Feel free to check out the application!