---
layout: default
title: "Recipe Ratings: Desserts vs. Non-Desserts"
---

<section class="hero">
  <div>
    <p class="eyebrow">DSC 80 Final Project</p>
    <h1>Dessert and Non-Dessert Recipe Ratings</h1>
    <p class="hero-copy">For this project, I compared ratings for dessert and non-dessert recipes from Food.com. I also made a model to predict whether a recipe's average rating will be at least 4.5.</p>
    <p class="byline">Raynard Taneka | DSC 80</p>
  </div>
</section>

<section class="section" id="intro">
  <div class="section-heading">
    <span class="section-number">Introduction</span>
    <div>
      <h2>The data and question</h2>
      <p>The original files have 83,782 recipes and 731,927 user interactions. After removing recipes without a valid rating, I had 81,173 recipes. I chose this question because people use ratings to decide what to make. Desserts are only 15.8% of the cleaned data, so I use percentages within each group instead of just comparing counts.</p>
    </div>
  </div>

  <table class="summary-table wide-table">
    <caption>Columns used for the main question</caption>
    <thead><tr><th>Column</th><th>What it contains</th></tr></thead>
    <tbody>
      <tr><td>id and recipe id</td><td>Keys used to match each recipe with its ratings</td></tr>
      <tr><td>rating</td><td>A user's rating; 0 represents a missing rating</td></tr>
      <tr><td>tags</td><td>Recipe labels used to identify desserts</td></tr>
      <tr><td>average rating</td><td>The mean of a recipe's non-missing ratings</td></tr>
      <tr><td>recipe type</td><td>My dessert or non-dessert label</td></tr>
    </tbody>
  </table>
</section>

<section class="section" id="explore">
  <div class="section-heading">
    <span class="section-number">Data and EDA</span>
    <div>
      <h2>Cleaning the data</h2>
      <p>I changed ratings of 0 to missing because the real rating scale is 1 to 5. Then I found the average rating for each recipe and merged it with the recipe table. I used the tags to label desserts, removed recipes with no average for this analysis, and made a high-rating column for averages of at least 4.5.</p>
    </div>
  </div>

  <table class="data-table">
    <caption>First five rows of selected cleaned columns</caption>
    <thead><tr><th>Name</th><th>Minutes</th><th>Steps</th><th>Ingredients</th><th>Average rating</th><th>Recipe type</th></tr></thead>
    <tbody>
      <tr><td>1 brownies in the world best ever</td><td>40</td><td>10</td><td>9</td><td>4.0</td><td>Dessert</td></tr>
      <tr><td>1 in canada chocolate chip cookies</td><td>45</td><td>12</td><td>11</td><td>5.0</td><td>Non-dessert</td></tr>
      <tr><td>412 broccoli casserole</td><td>40</td><td>6</td><td>9</td><td>5.0</td><td>Non-dessert</td></tr>
      <tr><td>millionaire pound cake</td><td>120</td><td>7</td><td>7</td><td>5.0</td><td>Dessert</td></tr>
      <tr><td>2000 meatloaf</td><td>90</td><td>17</td><td>13</td><td>5.0</td><td>Non-dessert</td></tr>
    </tbody>
  </table>

  <div class="chart-card">
    <div class="chart-title"><h3>Overall rating distribution</h3><p>Most average ratings are close to 5. About three quarters of the recipes have an average of at least 4.5.</p></div>
    <iframe class="chart-frame" src="assets/overall-rating.html" title="Distribution of all average recipe ratings"></iframe>
  </div>

  <div class="chart-card">
    <div class="chart-title"><h3>Ratings by recipe type</h3><p>Both groups are concentrated near 5, but the non-dessert distribution is slightly farther to the right. The bars show percentages within each recipe type because the group sizes are different.</p></div>
    <iframe class="chart-frame" src="assets/rating-distribution.html" title="Average rating distribution by recipe type"></iframe>
  </div>

  <div class="chart-card">
    <div class="chart-title"><h3>Ratings over time</h3><p>Average ratings changed across submission years for both recipe types. This suggests that submission year may contain useful information for prediction.</p></div>
    <iframe class="chart-frame short-chart" src="assets/rating-by-year.html" title="Mean average rating by submission year and recipe type"></iframe>
  </div>

  <table class="summary-table wide-table">
    <caption>Average rating grouped by recipe type</caption>
    <thead><tr><th>Recipe type</th><th>Recipe count</th><th>Mean rating</th><th>Median rating</th></tr></thead>
    <tbody>
      <tr><td>Dessert</td><td>12,868</td><td>4.583</td><td>5.000</td></tr>
      <tr><td>Non-dessert</td><td>68,305</td><td>4.633</td><td>5.000</td></tr>
    </tbody>
  </table>
  <p class="table-note">The medians are the same, while the non-dessert mean is about 0.05 points higher. This means the difference exists mainly in the lower part of the distributions.</p>
</section>

<section class="section" id="missingness">
  <div class="section-heading">
    <span class="section-number">Missingness</span>
    <div>
      <h2>Assessment of missingness</h2>
      <p>I think average rating may be <strong>MNAR</strong>. A recipe might not get rated because nobody made it, or someone might only rate it after a very good or bad result. If I had page views, saves, and the number of people who made each recipe, the missingness might be explainable and become MAR.</p>
    </div>
  </div>

  <p>I tested whether missingness in average rating depends on submission year and recipe-name length. I used the absolute difference in group means with 1,000 permutations and a 0.05 significance level.</p>
  <table class="summary-table wide-table">
    <caption>Missingness permutation tests</caption>
    <thead><tr><th>Comparison column</th><th>Observed statistic</th><th>p-value</th><th>Decision</th></tr></thead>
    <tbody>
      <tr><td>Submission year</td><td>0.730 years</td><td>0.0010</td><td>Depends on year</td></tr>
      <tr><td>Recipe-name length</td><td>0.082 characters</td><td>0.7033</td><td>No evidence of dependence</td></tr>
    </tbody>
  </table>
  <p class="table-note">Recipes without an average rating tend to have later submission years, so I reject the first null hypothesis. I fail to reject the name-length null hypothesis.</p>

  <div class="chart-card">
    <div class="chart-title"><h3>Missing ratings and submission year</h3><p>The distribution for recipes with missing ratings is shifted toward later years. This agrees with the small p-value from the submission-year test.</p></div>
    <iframe class="chart-frame short-chart" src="assets/missingness-year.html" title="Submission years for recipes with and without average ratings"></iframe>
  </div>
</section>

<section class="section" id="test">
  <div class="section-heading">
    <span class="section-number">Hypothesis test</span>
    <div><h2>Dessert and non-dessert ratings</h2><p>I used a one-sided permutation test with 2,000 repetitions and a significance level of 0.05.</p></div>
  </div>
  <div class="test-grid">
    <article class="hypothesis"><small>Null hypothesis</small><p>Dessert and non-dessert recipes come from the same distribution of average ratings. Any difference in their means is due to chance.</p></article>
    <article class="hypothesis"><small>Alternative hypothesis</small><p>Non-dessert recipes have a higher mean average rating than dessert recipes.</p></article>
    <article class="result-card"><h3>Result</h3><p>The test statistic was mean non-dessert rating minus mean dessert rating. The difference was 0.0509 and the p-value was 0.0005, so I reject the null hypothesis. Non-desserts have a slightly higher mean, but this does not show that recipe type caused the difference.</p></article>
  </div>
  <div class="chart-card">
    <div class="chart-title"><h3>Permutation results</h3><p>None of the simulated differences was as large as the observed difference shown by the red line.</p></div>
    <iframe class="chart-frame short-chart" src="assets/hypothesis-test.html" title="Permutation distribution for the dessert rating test"></iframe>
  </div>
</section>

<section class="section" id="model">
  <div class="section-heading">
    <span class="section-number">Prediction</span>
    <div>
      <h2>Predicting high-rated recipes</h2>
      <p>This is binary classification. The response is whether a recipe's average rating is at least 4.5. I only use information known when the recipe is posted, so ratings, reviews, and number of ratings are excluded.</p>
    </div>
  </div>
  <p>I use balanced accuracy because about 75% of recipes are high-rated. Unlike plain accuracy, balanced accuracy gives equal importance to correctly identifying high- and lower-rated recipes.</p>

  <h3>Baseline model</h3>
  <p>The baseline is logistic regression using three quantitative features: minutes, number of steps, and number of ingredients. I use the log of minutes because of its large outliers, then fill missing values and standardize the features in one sklearn pipeline.</p>
  <p>The training balanced accuracy is 0.519 and the test balanced accuracy is 0.518. Both scores are only slightly above 0.5, so this model underfits and is not very useful yet.</p>

  <h3>Final model</h3>
  <p>The final model keeps those three features and adds submission year, the seven nutrition values, and words from recipe names and tags. Year can capture changes over time, nutrition describes what is in the recipe, and the name and tags describe the kind of food. I convert the text columns to TF-IDF features and keep everything in one pipeline.</p>
  <p>I used three-fold cross-validation on the training set to compare regularization values of 0.05, 0.2, and 1. The best value was <code>C = 0.05</code>. The final training balanced accuracy is 0.584 and the test balanced accuracy is 0.572, an improvement of about 0.054 on the same test set.</p>

  <div class="chart-card">
    <div class="chart-title"><h3>Baseline compared with final model</h3><p>The added recipe information improves both training and test balanced accuracy. The train-test gap remains fairly small.</p></div>
    <iframe class="chart-frame short-chart" src="assets/model-comparison.html" title="Training and test balanced accuracy for baseline and final models"></iframe>
  </div>
</section>

<section class="section" id="fairness">
  <div class="section-heading">
    <span class="section-number">Fairness</span>
    <div>
      <h2>Does the model perform worse for desserts?</h2>
      <p>I compared dessert recipes (Group X) with non-dessert recipes (Group Y) because desserts are the smaller group. I kept the fitted final model fixed and permuted only the group labels 1,000 times.</p>
    </div>
  </div>
  <p><strong>Null hypothesis:</strong> The model's balanced accuracy is approximately equal for dessert and non-dessert recipes, and the difference is due to chance.</p>
  <p><strong>Alternative hypothesis:</strong> The model's balanced accuracy is lower for dessert recipes.</p>
  <p><strong>Test statistic:</strong> dessert balanced accuracy minus non-dessert balanced accuracy. The significance level is 0.05.</p>

  <table class="summary-table wide-table">
    <caption>Fairness test results</caption>
    <tbody>
      <tr><th>Dessert balanced accuracy</th><td>0.570</td></tr>
      <tr><th>Non-dessert balanced accuracy</th><td>0.572</td></tr>
      <tr><th>Observed difference</th><td>-0.002</td></tr>
      <tr><th>Permutation p-value</th><td>0.4496</td></tr>
    </tbody>
  </table>
  <p class="table-note">The p-value is larger than 0.05, so I fail to reject the null hypothesis. I do not have enough evidence that the model is worse for desserts. This only checks these two groups and this one metric.</p>

  <div class="chart-card">
    <div class="chart-title"><h3>Fairness permutation results</h3><p>The observed difference is near the center of the permutation distribution, which matches the large p-value.</p></div>
    <iframe class="chart-frame short-chart" src="assets/fairness-test.html" title="Permutation distribution for the fairness analysis"></iframe>
  </div>
</section>
