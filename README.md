
# Data Cleaning and Data Analysis of movies.csv

This repository deals with the data cleaning and univariate , bivariate and multivariate analysis on movies data set found in kaggle

---

## 1. Data Preparation and First Look

- **Collecting the Data:**\
  I started by importing the `movies.csv` file using pandas.

- **First Look:**\
  I used functions like `.head()`, `.info()`, and `.describe()` to quickly check:

  - How many rows and columns the dataset has
  - The overall data size and data types\
    This initial inspection helped me spot issues such as extra columns, missing values, and incorrect data formats.

---

## 2. Data Cleaning

### a. Dealing with Missing Values and Duplicates

- **Checking for Issues:**\
  I ran `.isnull()` to find missing values and `.duplicated()` to catch any duplicate records.

  - **Key Observation:** The "gross" column had almost 95% missing values.

- **Handling Missing Values:**

  - **Ratings:**\
    Missing ratings were replaced by calculating the average rating for each film genre. This way, if a movie didn’t have a rating, it received the average rating of its genre.

  - **Votes:**\
    For the votes column, I used a similar approach—except I grouped the data by cast details. By computing an average number of votes for each cast group, I filled in the missing entries.

- **Removing Duplicates:**\
  I removed duplicate observations to ensure every movie was only represented once, preventing any bias in the analysis.

### b. Data Type Conversions

- **Votes Column:**\
  The votes were initially stored as text (with commas). I stripped out the commas and converted these values into integers.

- **Other Conversions:**\
  I made sure that all numerical columns were properly formatted (as integers or decimals) and that date columns were converted to datetime objects when needed.

### c. Dropping and Engineering Columns

- **Removing the Gross Column:**\
  Since the "gross" column had nearly 95% missing values and little useful information, I dropped it from the dataset.

- **Splitting and Completing the Year Columns:**\
  I split the original year column into two new columns:

  - **From Year:** The year the movie started.
  - **To Year:** The year the movie ended.
    - If no end year was specified, I defaulted it to 2025.
    - If only one date was provided, I set both the "from" and "to" year to that same value.
  - For any missing values in these year columns, I calculated an average runtime from movies with complete data and used that average to fill the gaps.

- **Populating Missing Runtime:**\
  I used the "from year" and "to year" information to estimate an average runtime for movies within the same period, and then I filled in any missing runtime values accordingly.

### d. Last Data Review

After completing these cleaning steps, I did a final check for duplicates or blank values and removed any problematic rows. The result? A clean dataset of **6,745 rows and 9 columns**, all set for further analysis.

---

## 3. One-Variable (Univariate) Analysis

**Purpose:**\
To understand the distribution and key characteristics of each individual variable.

- **Histograms:**

  - I plotted histograms for continuous variables like rating, runtime, and revenue.
  - **Why:** Histograms show how many movies fall within specific value ranges and help identify if the data is skewed (e.g., many movies with low ratings and a few with very high ratings).

- **Box Plots:**

  - I used box plots to display the median, quartiles, and any remaining outliers.
  - **Why:** A neat box plot confirms that the data spread is controlled and that any extreme values have been appropriately handled.

- **Bar Charts:**

  - I created bar charts for categorical features like movie genres.
  - **Why:** Bar charts clearly show which genres are most common, offering a quick look at how the films are distributed across categories.

---

## 4. Bivariate Analysis

**Purpose:**\
To explore the relationships between pairs of variables.

- **Scatter Plots:**

  - I plotted pairs such as rating vs. runtime and rating vs. revenue.
  - **Why:** Scatter plots visually reveal if there’s any relationship between two continuous variables. A straight-line trend suggests a strong relationship, while a scattered plot points to a weak or non-linear one.

- **Grouped Bar Charts:**

  - I used grouped bar charts to compare average values across different groups (for example, average revenue per genre).
  - **Why:** These charts help identify trends—like which genres tend to earn more—which is valuable for market analysis and understanding audience preferences.

---

## 5. Multivariate Analysis

**Purpose:**\
To understand how several variables interact with each other at once.

- **Correlation Heatmap:**

  - I built a heatmap to measure the strength and direction of relationships between key numerical features (like rating, runtime, revenue, and votes).
  - **Why:** Each cell shows a correlation coefficient (from –1 to 1). In this case, most coefficients were low, meaning that changes in one variable do not strongly predict changes in another.

- **Pair Plots:**

  - I generated pair plots to visually inspect how every pair of variables interacts.
  - **Why:** These plots confirmed the heatmap’s findings by showing weak relationships and signs of multicollinearity—where some variables are redundant. This indicates that while the dataset is great for simpler analyses, it might need further work (or extra data) to support more complex multivariate models.

---

## 6. Overall Inferences

### Data Cleaning Summary

- **What Was Done:**
  - Removed unnecessary columns (like "gross") and duplicates.
  - Filled missing values carefully:
    - Ratings were imputed using genre averages.
    - Votes were imputed using cast details.
    - Year columns were completed using averages calculated from movies with full year data.
    - Runtime was filled using estimates from the "from year" and "to year" information.
  - Corrected data types and engineered new columns by splitting the year information.

### Analysis Takeaways

- **Univariate Analysis:**

  - Histograms and box plots revealed the distribution, skewness, and spread of each variable, with outliers handled appropriately.
  - Bar charts highlighted which film genres were most common.

- **Bivariate Analysis:**

  - Scatter plots and grouped bar charts illustrated pairwise relationships, though many relationships were relatively weak.

- **Multivariate Analysis:**

  - The correlation heatmap and pair plots showed generally weak relationships between variables and some multicollinearity, suggesting that the dataset is best suited for simpler analyses rather than complex multivariate models.

### Final Thoughts

By carefully cleaning and enriching the dataset—handling missing values with thoughtful strategies (using genre for ratings, cast details for votes, and calculated averages for year and runtime), removing duplicates, and creating useful new columns—I produced a dataset with **6,745 rows and 9 columns**. The univariate and bivariate analyses offered clear insights into individual distributions and pairwise relationships. However, the weak correlations and redundancy revealed in the multivariate analysis suggest that while the dataset is ready for simple analyses, it might need further refinement or additional data for robust multivariate modeling.

---

