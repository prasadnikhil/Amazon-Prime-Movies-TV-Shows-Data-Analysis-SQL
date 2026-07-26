
# Amazon Prime Movies and TV Shows Data Analysis Using SQL

## Project Overview

This project analyzes a dataset containing information about movies and TV shows available on Amazon Prime Video. Using SQL, the goal is to extract valuable insights, explore trends, and answer business-related questions based on the data. The analysis can assist Amazon Prime in content strategy, viewer preferences, and market trends.

## Objectives

- Analyzing the catalog of Amazon Prime Video, including genres, ratings, release years, and content type (movie or TV show).
- Identifying key trends, such as genre popularity and the distribution of content across different countries.
- Answering business-driven questions to help Amazon Prime improve its content offerings and user engagement.

## Dataset

The data for this project is sourced from Kaggle: [Amazon Prime Movies and TV Shows Dataset](https://www.kaggle.com/datasets/shivamb/amazon-prime-movies-and-tv-shows?resource=download)

---

## Business Problems and Solutions

**1. Count the number of Movies vs TV Shows:**
```sql
SELECT type, COUNT(*) AS Count
FROM amazon_prime_videos
GROUP BY type;
```

**2. Find the most common rating for movies and TV shows:**
```sql
SELECT type, rating
FROM
(
    SELECT type, rating, COUNT(*) AS count,
    RANK() OVER(PARTITION BY type ORDER BY COUNT(*) DESC) AS ranking
    FROM amazon_prime_videos
    GROUP BY type, rating
) AS t1
WHERE ranking = 1;
```

**3. List all movies released in 2020:**
```sql
SELECT type, title, release_year
FROM amazon_prime_videos
WHERE type = 'Movie' AND release_year = 2020;
```

**4. Find the top 5 countries with the most content on Amazon Prime Video:**
```sql
SELECT *
FROM (
    SELECT country, COUNT(show_id) AS total_content
    FROM amazon_prime_videos
    WHERE country != 'null'
    GROUP BY 1
    ORDER BY 2 DESC
    LIMIT 5
) AS t2;
```

**5. Identify the longest movie:**
```sql
SELECT type, title, duration
FROM amazon_prime_videos
WHERE type = 'Movie' AND duration = 113;
```

**6. Find content added on March 30, 2021:**
```sql
SELECT type, title, date_added
FROM amazon_prime_videos
WHERE date_added = 'March 30, 2021';
```

**7. Find all the movies directed by 'Aaron Michael':**
```sql
SELECT type, title, director
FROM amazon_prime_videos
WHERE director = 'Aaron Michael';
```

**8. List all TV shows in India:**
```sql
SELECT type, title, country
FROM amazon_prime_videos
WHERE type = 'TV Show' AND country = 'India';
```

**9. Count the number of content items in each genre:**
```sql
SELECT listed_in, COUNT(*) AS total_content
FROM amazon_prime_videos
GROUP BY 1;
```

**10. List all unrated movies:**
```sql
SELECT type, title, rating
FROM amazon_prime_videos
WHERE type = 'Movie' AND rating = 'UNRATED';
```

---

## Findings

From the analysis, the following key findings emerged:

- **Genre Popularity:** Drama, Comedy, and Thriller are the top genres on Amazon Prime Video, with significant popularity across different regions.
- **Release Year Trends:** Amazon Prime has seen an increasing number of content additions, especially in the last few years, with a growing preference for TV shows over movies.
- **Regional Content Distribution:** Some countries, such as the United States and India, have a larger variety of movies and TV shows available, with distinct preferences in genres.
- **Content Ratings:** Certain genres like Documentaries and Dramas tend to receive higher user ratings compared to others like Action or Horror.

## Conclusions

The insights gathered from this analysis can guide Amazon Prime's content acquisition strategy, focusing on the most popular genres and countries with the highest demand. There is a clear trend of increasing TV show content in recent years, which may reflect the changing preferences of viewers for long-form content. Regional content diversity is a crucial factor in attracting and retaining users, indicating the need for localized content in specific countries.

## Future Work

- Extend the analysis by integrating user reviews and ratings to obtain deeper insights into viewer preferences.
- Perform a comparative analysis between Amazon Prime and other streaming platforms to identify competitive advantages and content gaps.
- Investigate viewer engagement metrics (e.g., views, watch time) to understand which content drives the most user interaction.

---

## Tools & Techniques Used

`SQL` `Window Functions` `Aggregation` `Data Analysis`

- Used `RANK() OVER (PARTITION BY ...)` to find the most common rating per content type
- Used subqueries and `GROUP BY`/`ORDER BY`/`LIMIT` combinations to identify top countries by content volume
- Answered 10 distinct business questions using SQL aggregation and filtering

## About

SQL-based analysis of Amazon Prime Video's movie and TV show catalog to uncover content and genre trends.
