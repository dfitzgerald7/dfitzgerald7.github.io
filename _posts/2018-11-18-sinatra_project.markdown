---
layout: post
title:      "Sinatra Project "
date:       2018-11-18 10:44:11 -0500
permalink:  sinatra_project
---


For the second project in the software engineer bootcamp, I needed to create an app using sinatra that tracked something. This app needed to use the MVC pattern and implement CRUD functions. My app revolves around the NBA. It allows users to store their favorite teams and vote for their favorite players. The cummulative votes are stored across all users, and the most popular players are displayed on the leaderboard page. 
There were 3 main objects in this app. The User, storing all the account information, the Team, storing all the players, and the Player itself. The User and the Team objects both have many of each other. This allows the app to have unique Team objects. If the same team belongs to two different users and one user votes on a certain player, that vote is shown to both users. A join table was necessary to connect the User and Team objects. 
The user info is important as it limits what info can be seen. While a user can see all of the players and their votes, they can only vote on a player who is on a team that they declare as their favorite. A user can also only delete a player that they created. 
As of writing this, I plan on adding the functionality of limiting votes to one per day per user. I also hope to add a web scraping component. My original idea involved all of the team objects knowing who their starting 5 players are so that they can be displayed and voted on once a user chooses that team. I decided not to not include that in the original version, and instead allow users to add players. 
