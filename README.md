# Data Cleaning and Analysis of movies.csv

This repository covers the data cleaning and analysis of the movies dataset from Kaggle. It includes univariate, bivariate, and multivariate analysis to understand the characteristics and relationships in the data.

---

## 1. Data Preparation and First Look

### Collecting the Data
- Imported the **movies.csv** file using pandas.

### First Look
- Used `.head()`, `.info()`, and `.describe()` to quickly check:
  - Number of rows and columns.
  - Data types and overall size.
- This helped identify issues such as extra columns, missing values, and incorrect formats.

---

## 2. Data Cleaning

### a. Handling Missing Values and Duplicates
- **Checking for Issues:**
  - Used `.isnull()` to identify missing values.
  - Used `.duplicated()` to find duplicate records.
- **Key Observation:**
  - The "gross" column had almost 95% missing values.
- **Handling Missing Data:**
  - **Ratings:** Missing ratings were filled with the average rating of the movie’s genre.
  - **Votes:** Filled missing votes by calculating the average votes for each cast group.
- **Removing Duplicates:**
  - Duplicate entries were removed to ensure each movie appears only once.

### b. Data Type Conversions
- **Votes Column:**
  - Removed commas and converted votes from text to integers.
- **Other Conversions:**
  - Ensured numerical columns were properly formatted.
  - Converted date columns to datetime objects when needed.

### c. Dropping and Engineering Columns
- **Removing the Gross Column:**
  - Dropped due to excessive missing values.
- **Year Columns:**
  - Split the original year column into “From Year” (start) and “To Year” (end).
  - Defaulted missing end years to 2025 and set single year entries to both columns.
- **Populating Missing Runtime:**
  - Estimated runtime based on "From Year" and "To Year" data and filled in missing values.

### d. Final Data Review
- Conducted a final check to remove any remaining duplicates or blank rows.
- **Clean Dataset:** 6,745 rows and 9 columns ready for analysis.

---

## 3. Univariate Analysis

The goal was to understand the distribution and key features of individual variables.

### Histograms & Box Plots (Continuous Variables)
- **Histograms:**  
  - Plotted for rating, runtime, and revenue to show the data distribution.
- **Box Plots:**  
  - Highlighted medians, quartiles, and outliers.

### Bar Charts (Categorical Variables)
- **Bar Charts:**  
  - Used for genres to show the frequency of each category.

### Key Findings

#### A. Movie Ratings
- **Distribution:**  
  - KDE plot shows a single peak with most ratings between 5 and 8, peaking around 7.
- **Interpretation:**  
  - Most movies get average to good ratings; very few receive extreme scores.
- **Central Tendency:**  
  - **Mean:** 6.63  
  - **Median:** 6.70  
  - **Mode:** 7.20 (suggested by the KDE peak)
- **Skewness:**  
  - Slightly left-skewed due to a few very low ratings.

#### B. Votes
- **Distribution:**  
  - Highly right-skewed: most movies have few votes, while a few blockbusters get millions.
- **Interpretation:**  
  - A few movies gain mass attention, while most have limited engagement.
- **Central Tendency:**  
  - **Mean:** 20,385 votes  
  - **Median:** 1,975 votes  
  - **Mode:** ~20,385 votes (influenced by blockbusters)
- **Skewness:**  
  - Extremely right-skewed with a long tail.

#### C. Runtime
- **Distribution:**  
  - Most movies run between 80 and 120 minutes, though the mean is lower (~77.94 minutes) due to some very short and very long movies.
- **Interpretation:**  
  - Indicates the typical film length; outliers include short films and extended features.
- **Central Tendency:**  
  - **Mean:** 77.94 minutes  
  - **Median:** 81 minutes  
  - **Mode:** 90.56 minutes
- **Skewness:**  
  - Right-skewed with long outliers affecting the mean.

#### D. Genres
- **Findings:**  
  - **Drama** is the most common genre, followed by **Comedy** and **Action**.
  - Genres like **Musical**, **Game-Show**, **Talk-Show**, **News**, and **Film-Noir** are less frequent.
- **Interpretation:**  
  - Dominance of Drama suggests a focus on storytelling, while Comedy and Action are popular for their wide appeal.

---

## 4. Bivariate Analysis

Explored relationships between pairs of variables using scatter plots, 2D histograms, density plots, KDE plots, bar graphs, and box plots.

### Key Relationships

1. **Rating vs. Votes**
   - **Plot & Correlation:**  
     - Scatter plot shows a wide spread with a weak positive correlation (~0.10).
   - **Interpretation:**  
     - Higher-rated movies tend to get slightly more votes, but many other factors influence popularity.

2. **Rating vs. Runtime**
   - **Plot & Correlation:**  
     - Weak negative correlation (~-0.26) with a scattered plot.
   - **Interpretation:**  
     - Longer movies tend to have slightly lower ratings, but runtime alone doesn't strongly affect quality.

3. **Votes vs. Runtime**
   - **Plot & Correlation:**  
     - Near-zero correlation (~0.09).
   - **Interpretation:**  
     - The number of votes is not affected by a movie’s length, suggesting other factors drive popularity.

4. **Genre vs. Rating**
   - **Box Plot:**  
     - Shows how ratings vary across genres.
   - **Interpretation:**  
     - Some genres (e.g., Documentary, Drama) have higher median ratings; others show more variability.

5. **Genre vs. Votes**
   - **Box Plot:**  
     - Highlights vote counts by genre.
   - **Interpretation:**  
     - Mainstream genres like Action and Adventure attract more votes; niche genres get fewer.

6. **Genre vs. Runtime**
   - **Box Plot:**  
     - Compares runtime across genres.
   - **Interpretation:**  
     - Certain genres (e.g., Documentary) tend to be shorter, while others (e.g., War, Sci-Fi) are longer.

7. **Year Difference vs. Runtime**
   - **Bar Plot:**  
     - Shows how runtime may change with the movie's age.
   - **Interpretation:**  
     - Older movies might be shorter due to past trends, or newer films might be longer; the pattern is not clear-cut.

---

## 5. Multivariate Analysis

Used advanced methods like correlation heat maps, pair plots, 3D scatter plots, PCA, and clustering.

### Findings

- **Correlation Analysis:**  
  - Very low correlations between **RATING**, **VOTES**, and **Runtime** (near-zero values).
  - **Interpretation:**  
    - Each variable is almost independent; knowing one does not help predict another.

- **PCA (Principal Component Analysis):**  
  - Explained variance is nearly evenly distributed:
    - **PC1:** 34.28%
    - **PC2:** 33.61%
    - **PC3:** 32.11%
  - **Interpretation:**  
    - No single component captures most of the variance; the variables are independent, and PCA doesn’t reduce dimensions effectively.

- **PCA Visualization:**  
  - A 2D scatter plot of **RATING** against **PC1** and **PC2** shows a gradient but no clear clusters.
  - **Interpretation:**  
    - The apparent gradient is misleading; there are no distinct groups.

- **Clustering:**  
  - K-Means clustering (with 2 clusters) resulted in a low silhouette score (0.237).
  - **Interpretation:**  
    - Poor cluster separation indicates that natural groupings are not present in the dataset.

- **Overall Interpretation:**  
  - The key movie attributes are independent and not strongly related.
  - Traditional multivariate methods like PCA and clustering do not uncover meaningful patterns here.

---

## Conclusion

Univariate,Bivariate,Multivariate analysis reveals that the main features of the movies dataset—ratings, votes, and runtime—mostly operate independently. While ratings generally fall in the moderate range and runtimes cluster around standard lengths, votes are extremely skewed due to a few blockbuster movies. Bivariate analysis shows only weak links among these variables, and multivariate techniques like PCA and clustering fail to extract strong underlying patterns. In short, each attribute appears to be influenced by its own set of factors, making it challenging to find hidden relationships using standard multivariate methods.
"""

