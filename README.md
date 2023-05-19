---
layout: page
title: Project 3
description: Description of Project 3.
nav_exclude: true
---

# Better Recipes are Shorter Recipes
We will explore a dataset with information regarding food reviews from food.com. I will specifically be answering the question: Do shorter recipes tend to recieve higher ratings? So if you want high reviews on a recipe you are posting, maybe think about how long it takes to make.

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

| name                                 |     id |   minutes | tags                                                                                                                                                                                                                        |   n_steps |   n_ingredients |   rating |   rating_avg |
|:-------------------------------------|-------:|----------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------:|----------------:|---------:|-------------:|
| 1 brownies in the world    best ever | 333281 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] |        10 |               9 |        4 |            4 |
| 1 in canada chocolate chip cookies   | 453467 |        45 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               |        12 |              11 |        5 |            5 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        5 |            5 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        5 |            5 |
| 412 broccoli casserole               | 306168 |        40 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |         6 |               9 |        5 |            5 |


---



