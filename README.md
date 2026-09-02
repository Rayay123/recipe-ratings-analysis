# Dessert and Non-Dessert Recipe Ratings

This is my DSC 80 final project using recipe and rating data from Food.com.

[View the project website](https://rayay123.github.io/recipe-ratings-analysis/)

## Project Question

I wanted to see whether dessert recipes receive different ratings from non-dessert recipes. I also wanted to build a model that predicts whether a recipe will have a high average rating using information available when the recipe is posted.

## Data

The cleaned dataset contains 81,173 recipes. I treated ratings of 0 as missing and calculated one average rating for each recipe. Dessert recipes were identified using the recipe tags. Since desserts only make up about 15.8% of the recipes, I compared percentages within each group instead of comparing raw counts.

## Hypothesis Test

I ran a one-sided permutation test comparing the mean ratings of dessert and non-dessert recipes. Non-dessert recipes had an average rating of 4.633, while dessert recipes had an average rating of 4.583. The p-value was 0.0005, so I rejected the null hypothesis. The difference was statistically significant, but it was only about 0.05 rating points.

## Baseline Model

My baseline model is logistic regression. It uses recipe minutes, number of steps, and number of ingredients to predict whether the average rating is at least 4.5. The test balanced accuracy was 0.518. For the final model, I plan to add nutrition, tag, ingredient, and submission-year information.

## Current Progress

The data cleaning, exploratory analysis, hypothesis test, prediction problem, and baseline model are complete. The final model and fairness analysis will be added for the final submission.
