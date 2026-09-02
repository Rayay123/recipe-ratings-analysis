# Beyond the Dessert Aisle: What Shapes Recipe Ratings?

**Raynard Taneka**

## Introduction

This project uses Food.com recipe and rating data to ask whether dessert recipes have different average ratings than non-dessert recipes. Dessert recipes are less common than non-dessert recipes, so the analysis compares distributions within each group rather than relying on raw counts.

## Data Cleaning and Exploratory Data Analysis

## Assessment of Missingness

## Hypothesis Testing

I tested whether the average recipe rating is the same for dessert and non-dessert recipes.

- Null hypothesis: Dessert status is unrelated to average recipe rating; observed differences are due to chance.
- Alternative hypothesis: Non-dessert recipes have a higher average rating than dessert recipes.
- Test statistic: mean non-dessert rating minus mean dessert rating.

After treating 0 ratings as missing and averaging ratings by recipe, desserts had a mean rating of 4.583 and non-desserts had a mean rating of 4.633. The observed difference was 0.0509 rating points. In 2,000 permutations that shuffled the recipe-type labels while keeping the original group sizes fixed, no simulated difference was as large. The permutation p-value was 0.0005, so I reject the null hypothesis at the 0.05 significance level. The difference is statistically significant but small in rating units.

<iframe src="assets/dessert_rating_distribution.html" width="980" height="600" frameborder="0"></iframe>

## Framing a Prediction Problem

The prediction task is binary classification: predict `high_rating`, whether a recipe's average rating is at least 4.5. Since about 75% of recipes meet this definition, I use balanced accuracy as the main evaluation metric so performance on the lower-rated recipes is not ignored.

## Baseline Model

The baseline is a logistic-regression classifier using recipe details known before anyone submits a rating: `minutes`, `n_steps`, and `n_ingredients`. `minutes` is log-transformed because it is highly right-skewed; all numerical features are imputed and standardized in one sklearn pipeline. The data is split into 75% training and 25% testing data with stratification by `high_rating`.

The baseline test balanced accuracy is 0.518. This is only slightly above random performance, so it is not a strong model yet. I plan to improve it using recipe-side information that could plausibly affect ratings, including parsed nutrition values, recipe tags, ingredient count patterns, and the year the recipe was submitted. I will tune at least one model hyperparameter with cross-validation.

## Final Model

## Fairness Analysis
