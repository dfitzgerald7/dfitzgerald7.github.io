---
layout: post
title:      "RESTaurants: My Rails Portfolio Project"
date:       2019-01-06 20:08:00 +0000
permalink:  restaurants_my_rails_portfolio_project
---


For my Rails porfolio project, I created a restaurant review app similar to Yelp. The app revolves around users leaving a rating and a review for a given restaurant. A user can then view a list of all restaurants that have be reviewed, ordered by their rating. 
The app is structured by three models, the restaurant, the review, and the user. The review acts as a join table, as the restaurant and user have a has many through relationship in both directions. The review requires the user to submit a rating and review. The restaurant objects are unique, so a given object can have many reviews and thus many users. Having unique restaurant objects allowed me to create the top-rated page, which used a class scope method for the ordering. 
A difficult aspect of this project was adding the Github login through oauth. The curriculum covered how to connect it to Facebook, but I wanted to use another website. There was limited documentation available for the "omniauth-github" gem itself, so I mostly tried to adapt the curriculum info. One issue was that the "auth" hash that is passed into the controller did not contain any info other than a username. Since my User validations require a password and email, I decided to create a User object with fake info for those two fields. I am still hoping to figure out how to pass more info with that hash. 
