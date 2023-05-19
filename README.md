---
layout: page
title: Better Recipes are Shorter Recipes
description: Better Recipes are Shorter Recipes
nav_exclude: true
---

# Better Recipes are Shorter Recipes
We will explore a dataset with information regarding food reviews from food.com. I will specifically be answering the question: Do recipes which take less time to make tend to recieve higher ratings? So if you want high reviews on a recipe you are posting, maybe think about how long it takes to make.

### Dataset Information
Our dataset has a total of 234,429 rows and 23 columns. Our relavent columns include:
- name: name of recipe
- id: uniqie identification number of recipe
- minutes: minutes it takes to make recipe
- tags: tags for recipe
- n_steps: number of steps the recipe takes to make
- n_ingredients: number of ingredients in recipe
- rating: rating of review
- rating_avg: avg rating given for recipe
remaining columns include PDV (percentage of daily value) values for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates.

## Cleaning and EDA
- Our data came from two datasets which had to be merged so that all the relavent columns were in one dataframe. 
- I replaced all ratings with values of 0 with nan values because we do not wan't these values to impact our analyses as I assume that they are place holders for ratings that were not made and not actual values.
- I made another column named 'rating_avg' so I could see the rating average of the recipe instead of just the single reviewers' rating.
- The 'tags' column had values which looked like lists but were actually strings, so I converted those strings into actual lists with each list entry being a string of the tag.
- The 'nutrition' column was also a string that looked like a list. So I converted the strings intro lists and made new columns for the nutrition values including, calories, protein, total fat, etc.

---

| name                                 |     id |   minutes | tags                                                                                                                                                                                                                        |   n_steps |   n_ingredients |   rating |   rating_avg |   calories |
|:-------------------------------------|-------:|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|----------------:|---------:|-------------:|-----------:|
| 1 brownies in the world    best ever | 333281 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] |        10 |               9 |        4 |            4 |      138.4 |
| 1 in canada chocolate chip cookies   | 453467 |        45 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               |        12 |              11 |        5 |            5 |      595.1 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        5 |            5 |      194.8 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        5 |            5 |      194.8 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        5 |            5 |      194.8 |

---


### Univariate Analysis

<iframe src="assets/Distribution-of-minutes.html" width=800 height=600 frameBorder=0></iframe>

Our first plot of the minute distribution showed some incredible outliers (over 1 million minute recipes) so I had to restrict the data frame to recipes under 5 hours. The distribution shows spikes in incriments of 5. This could be because people round their cooking times when posting reviews or recipes. 30 minutes is the most common recipe time.

### Bivariate Analysis



This plot shows for each rating, the average time it takes to make the meal goes down. The rating of 5 has the lowest average time to make its recipes.


### Interesting Aggregates

'|     1.0 |     2.0 |    3.0 |     4.0 |     5.0 |\n|--------:|--------:|-------:|--------:|--------:|\n| 48.8497 | 48.8552 | 46.548 | 43.3839 | 43.0632 |'

The mean for minutes taken is the lowest for ratings of 5.


## Assessment of Missingness

The rating column could be NMAR because when poeple post their own recipes I doubt they are rating it as well. So I would think that recipe submissions closer to 2008 had more missing ratings because people were posting their original recipes and not giving reviews.

### Missingness dependency


From this plot, we can see there is some difference between the date of submissions when the rating is missing and when the rating is included. So is this due to random chance or could another column be the reason we see a difference?

I used a ks-statistic to measure the farthest distance in our cumulative distribution functions for submission dates with ratings and without ratings. I did this by grouping the rows by missingness of rating and applying the ks-statistic method.

Observed ks-statistic: 0.05580897823545494

Then I did permutation sumulations to see how extreme this value is compared to simulated distributions of the ks-statistic.



P-Value: 0.0015469194250300686

I did not observe many simulations in which the ks-statistic was as extreme as our observed statistic. Thus we can conclude that the missingness of rating is not due to random chance and submission time may be a column upon which rating missingness is dependent on.


However, the missingness of rating was not dependent on the sodium column. Here I observed a p-value of 0.5313155076819254. This means my simulations observed a ks-statistic as extreme or more extreme as our observed ks-statistic around 53% of the time. Thus, the missingness of rating does not depend on how much sodium is in the recipe.


# Hypothesis Testing

'|    mean |   count |\n|--------:|--------:|\n| 4.68662 |  167548 |\n| 4.65804 |   51845 |'

Null Hypothesis: Cooking time of the recipe has no impact on the ratings of the recipe.

Alternative Hypothesis: Cooking time under 60 minutes leads to higher ratings of the recipe.

Test Statistic: The difference in means between ratings of recipes with cooking time under 60 minutes and over 60 minutes.

Significance Level: 0.01

Resulting P-Value: 0.0

In my hypothesis testing I used a permutation test to see if my two samples came from the same distribution or not. I used the difference in means test statistic because I needed to compare two distributions with the same shape. Our observed difference in means = 0.02858276372914048. Our closes observed simulated difference in mean value = 0.011768799556302945. Thus none of our simulated values were as extreme or more extreme than our observed value and I reject the null hypothesis. Cooking time under 60 seconds may increase your chance at a slightly higher rating.











