---
layout: default
title: "Recipe Ratings: Desserts vs. Non-Desserts"
---

<section class="hero">
  <div>
    <p class="eyebrow">Food.com Recipes and Ratings</p>
    <h1>Do dessert recipes receive different ratings?</h1>
    <h2 class="intro-heading">Introduction</h2>
    <p class="hero-copy">For this project, I looked at 81,173 recipes from Food.com. I compared dessert and non-dessert ratings, tested whether the difference was significant, and built a baseline model to predict whether a recipe will be highly rated.</p>
    <p class="byline">Raynard Taneka | DSC 80</p>
  </div>
</section>

<section class="section" id="explore">
  <div class="section-heading">
    <span class="section-number">Data and EDA</span>
    <div>
      <h2>Data Cleaning and Exploratory Data Analysis</h2>
      <p>I treated ratings of 0 as missing, averaged the remaining ratings for each recipe, and identified desserts using the recipe tags. Since there are many more non-dessert recipes, the chart uses percentages within each group instead of raw counts.</p>
    </div>
  </div>

  <table class="summary-table">
    <caption>Dataset summary</caption>
    <tbody>
      <tr><th scope="row">Recipes analyzed</th><td>81,173</td></tr>
      <tr><th scope="row">Dessert recipes</th><td>12,868</td></tr>
      <tr><th scope="row">Dessert share</th><td>15.8%</td></tr>
      <tr><th scope="row">Ratings of 0</th><td>Treated as missing</td></tr>
    </tbody>
  </table>

  <div class="chart-card">
    <div class="chart-title">
      <h3>Distribution of average ratings</h3>
      <p>Both groups are concentrated near five stars. Hover over the bars to see the percentages and recipe counts.</p>
    </div>
    <iframe class="chart-frame" src="assets/rating-distribution.html?v=2" title="Distribution of average recipe ratings for dessert and non-dessert recipes"></iframe>
  </div>
</section>

<section class="section" id="missingness">
  <div class="section-heading">
    <span class="section-number">Missingness</span>
    <div>
      <h2>Assessment of Missingness</h2>
      <p>In the Food.com data, a rating of 0 represents a missing rating rather than a real zero-star review, so I replaced these values with missing values before calculating recipe averages. The final project will also test whether missing descriptions depend on other recipe characteristics.</p>
    </div>
  </div>
</section>

<section class="section" id="test">
  <div class="section-heading">
    <span class="section-number">Hypothesis test</span>
    <div>
      <h2>Hypothesis Testing</h2>
      <p>I used a one-sided permutation test to check whether non-dessert recipes tend to receive higher average ratings than dessert recipes.</p>
    </div>
  </div>

  <div class="test-grid">
    <article class="hypothesis"><small>Null hypothesis</small><p>Dessert and non-dessert recipes have the same average rating. Any observed difference is due to chance.</p></article>
    <article class="hypothesis"><small>Alternative hypothesis</small><p>Non-dessert recipes have a higher average rating than dessert recipes.</p></article>
    <article class="result-card">
      <div><h3>Test result</h3><p>The p-value was 0.0005, so I rejected the null hypothesis at the 0.05 significance level. The observed difference was 0.0509 rating points after 2,000 permutations. This gives evidence that non-dessert recipes have a higher mean rating, but the difference itself is small.</p><p class="test-stat"><strong>Test statistic:</strong> mean(non-dessert) - mean(dessert)</p></div>
    </article>
  </div>
</section>

<section class="section" id="model">
  <div class="section-heading">
    <span class="section-number">Prediction</span>
    <div>
      <h2>Framing a Prediction Problem</h2>
      <p>My prediction task is binary classification. I predict whether a recipe's average rating will be at least 4.5 using only information available when the recipe is posted.</p>
    </div>
  </div>

</section>

<section class="section" id="baseline">
  <div class="section-heading">
    <span class="section-number">Current model</span>
    <div><h2>Baseline Model</h2><p>I started with logistic regression so I could compare later models against a simple, interpretable baseline.</p></div>
  </div>
  <div class="baseline-details">
    <h3>Model and features</h3>
    <p>I used logistic regression with recipe minutes, number of steps, and number of ingredients. I log-transformed the minutes column, filled in missing numerical values, and standardized the three features in one sklearn pipeline.</p>
    <h3>Evaluation</h3>
    <p>The test balanced accuracy was 0.518. I used balanced accuracy because about 75% of the recipes are in the high-rating class. The score is only a little better than random guessing across the two classes, so there is room to improve the model.</p>
  </div>
</section>

<section class="section" id="final-model">
  <div class="section-heading">
    <span class="section-number">Next step</span>
    <div><h2>Final Model</h2><p>For the final submission, I plan to add nutrition values, recipe tags, ingredient information, and submission year. I will compare a tree-based classifier with the baseline and tune at least one hyperparameter using cross-validation.</p></div>
  </div>
</section>

<section class="section" id="fairness">
  <div class="section-heading">
    <span class="section-number">Next step</span>
    <div><h2>Fairness Analysis</h2><p>After choosing the final model, I will compare its performance across two recipe groups with a permutation test. This section will be completed after the final model is fitted.</p></div>
  </div>
</section>
