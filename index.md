---
layout: default
title: "Beyond the Dessert Aisle"
---

<section class="hero">
  <div>
    <p class="eyebrow">Food.com recipe analysis</p>
    <h1>Beyond the <em>Dessert</em> Aisle</h1>
    <p class="hero-copy">Do desserts earn different ratings than the rest of the recipe box? This project follows 81,173 Food.com recipes from raw ratings to hypothesis testing and prediction.</p>
    <div class="author"><span class="author-mark">RT</span><span>Raynard Taneka · DSC 80</span></div>
  </div>
  <aside class="hero-note">
    <strong>A small gap, a big dataset.</strong>
    <p>Non-dessert recipes average 4.633 stars, compared with 4.583 for desserts. The difference is statistically clear but practically modest.</p>
  </aside>
</section>

<section class="section" id="explore">
  <div class="section-heading">
    <span class="section-number">01 · Explore</span>
    <div>
      <h2>Data Cleaning and Exploratory Data Analysis</h2>
      <p>I treated ratings of 0 as missing, averaged the remaining ratings for each recipe, and identified desserts through the recipe tags. Because desserts are the smaller group, every bar below shows the percentage within its own recipe type.</p>
    </div>
  </div>

  <div class="stat-grid">
    <div class="stat-card teal"><span>Recipes analyzed</span><strong>81,173</strong></div>
    <div class="stat-card"><span>Dessert recipes</span><strong>12,868</strong></div>
    <div class="stat-card"><span>Dessert share</span><strong>15.8%</strong></div>
    <div class="stat-card"><span>Zero ratings</span><strong>Missing</strong></div>
  </div>

  <div class="chart-card">
    <div class="chart-title">
      <h3>Where the ratings fall</h3>
      <p>The distributions look similar, with both groups concentrated near five stars. Hover over a bar for its exact percentage and recipe count.</p>
    </div>
    <iframe class="chart-frame" src="assets/dessert_rating_distribution.html" title="Distribution of average recipe ratings for dessert and non-dessert recipes"></iframe>
  </div>
</section>

<section class="section" id="missingness">
  <div class="section-heading">
    <span class="section-number">02 · Missingness</span>
    <div>
      <h2>Assessment of Missingness</h2>
      <p>The full missingness assessment will test whether missing descriptions depend on observable recipe characteristics. For the current rating analysis, Food.com rating values of 0 are treated as missing rather than genuine zero-star reviews.</p>
    </div>
  </div>
</section>

<section class="section" id="test">
  <div class="section-heading">
    <span class="section-number">03 · Test</span>
    <div>
      <h2>Hypothesis Testing</h2>
      <p>A one-sided permutation test asks whether the observed mean-rating gap could reasonably appear if dessert status and rating were unrelated.</p>
    </div>
  </div>

  <div class="test-grid">
    <article class="hypothesis"><small>Null hypothesis</small><h3>No relationship</h3><p>Dessert status is unrelated to average recipe rating. Any observed difference is due to chance.</p></article>
    <article class="hypothesis"><small>Alternative hypothesis</small><h3>Non-desserts rate higher</h3><p>Non-dessert recipes have a higher average rating than dessert recipes.</p></article>
    <article class="result-card">
      <div class="result-number">p = .0005</div>
      <div><h3>Reject the null hypothesis</h3><p>The observed difference was 0.0509 rating points after 2,000 label permutations. The evidence supports a higher mean for non-desserts, although the effect size is small.</p><span class="metric-pill">Test statistic: mean(non-dessert) − mean(dessert)</span></div>
    </article>
  </div>
</section>

<section class="section" id="model">
  <div class="section-heading">
    <span class="section-number">04 · Predict</span>
    <div>
      <h2>Framing a Prediction Problem</h2>
      <p>The prediction task is binary classification: predict whether a recipe will earn an average rating of at least 4.5 using only information available when the recipe is posted.</p>
    </div>
  </div>

  <div class="model-grid">
    <article class="model-card highlight"><small>Baseline model</small><h3>Logistic regression</h3><p>The model uses three quantitative recipe features in one sklearn pipeline. Minutes are log-transformed, then all features are imputed and standardized.</p><div class="feature-list"><code>minutes</code><code>n_steps</code><code>n_ingredients</code></div></article>
    <article class="model-card"><small>Evaluation</small><h3>Balanced accuracy: 0.518</h3><p>About 75% of recipes are labeled high rating, so balanced accuracy gives both classes equal importance. The baseline is only slightly above random performance across the two classes.</p></article>
  </div>
</section>

<section class="section" id="next">
  <div class="section-heading">
    <span class="section-number">05 · Next</span>
    <div><h2>The final analysis</h2><p>These sections will be completed for the final submission after feature engineering and model evaluation.</p></div>
  </div>
  <div class="next-grid">
    <article class="next-card"><small>Final Model</small><h3>Richer recipe signals</h3><p>Nutrition values, recipe tags, ingredient patterns, and submission year will be engineered and tested with cross-validation.</p></article>
    <article class="next-card"><small>Fairness Analysis</small><h3>Performance across groups</h3><p>The final fitted model will be compared across an interesting pair of recipe groups using a permutation test.</p></article>
  </div>
</section>
