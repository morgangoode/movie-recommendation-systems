# **Movie Recommendation System**
![the answer to the cold start problem](./images/movie-recommendation-system-bluf.png)

Flatiron School Phase 4 Data Science Project

## Team Members:

*  [Justin Phan](https://www.linkedin.com/in/vinh-phan427), Technical Lead

*  [Morgan Goode](https://www.linkedin.com/in/morgangoode/), GitHub/Presentation Lead

## Project Links

*   [Jupyter Notebook](https://github.com/morgangoode/movie-recommendation-systems/blob/morgan/movie_recommendation_systems.ipynb) 
*   [Presentation](https://github.com/morgangoode/movie-recommendation-systems/blob/morgan/movie-recommendation-systems-presentation.pdf)


# Business Understanding

## Stakeholder + Background:
![likewise app banner logo](./images/LWBanner_1584X396.jpg)
With over 6.5 million users, Likewise is the biggest app of its kind and wants to stay ahead of the game with its recommendation systems. While Likewise is also a social platform, people join the app primarily to get recommendations on what to watch or read so recommendations are their bread and butter. 

## Our Goal:
In this hypothetical scenario, our team has been tasked with improving the cold start experience when it comes to movie recommendations by building a model that provides top 5 movie recommendations to a user

# Data Overview
Our data comes from the popular MovieLens Dataset that includes a little over 100,000 ratings from 610 users on movies released from 1996-2018. Our target feature ‘rating’ has values from .5 - 5 stars and is what we used to perform our analysis. 

Limitations include the size of the dataset, as well as a date range that cuts off in September 2018.

## Methods

### Model Iterations + Creating New Features 
First we iterated on multiple matrix factorization models using the `Surprise` library. `Surprise`    is limited to 3 column dataframes as it's specifically designed for collaborative filtering and doesn't directly support incorporating additional features. Next, we built a hybrid content and collaborative XGBoost model with new features that outperformed our previous matrix factorization models:

`user_bias` calculates how much each user's mean movie rating  deviates from the global mean movie rating 

`item_bias` calculates how much each movie's mean rating deviates from the global mean movie rating

Collaborative data comes from the 'userId' and 'movieId' features. These identifiers allow the model to learn from the interactions between users and movies. 

Content data comes from the 'rating_user_bias' and ‘rating_item _bias' features. These are calculated based on the specific characteristics of users and movies.

## Results

Our final XGBoost model has a RMSE of .79, which is an improvement over our best performing matrix factorization model, which had an RMSE of .88. This means that, on average, our final model’s predicted movie rating is off by .79 stars.

## Conclusions
The bias features we created were key pieces of improving the model’s performance.

Super users also provided key input (RMSE increased when we filtered them out), but as the majority of the ratings came from a smaller group of super users this could also lead to overfitting. 


## Next steps

Get a larger dataset with evenly distributed user activity in order to improve predictions.

Adopt a more robust two-step approach to optimize content and collaborative filtering:

The limitations of matrix factorization— it struggles to make accurate recommendations when you have a lot of users and movies but not a lot of ratings —can be addressed by taking a two step approach:

Step 1:  Use collaborative filtering to generate a shortlist of recommendations. 
Step 2:  Use a more flexible model like a neural network to rank the shortlist. 

This ranking model can incorporate a wide variety of features, including the kinds of user and movie biases we’ve calculated. Many state-of-the-art recommender systems in industry employ such a solution.

## For more information
See the full analysis in the Jupyter Notebook or review this  [presentation](https://github.com/morgangoode/movie-recommendation-systems/blob/morgan/movie-recommendation-systems-presentation.pdf).

## Repository Structure

```
├── data
├── images
├── README.md
├── movie-recommendation-systems-presentation.pdf
└── movie-recommendation-systems.ipynb
```

