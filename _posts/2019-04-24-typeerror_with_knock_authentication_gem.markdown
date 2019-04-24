---
layout: post
title:      "TypeError with Knock Authentication Gem"
date:       2019-04-24 20:12:01 +0000
permalink:  typeerror_with_knock_authentication_gem
---


My final project at Flatiron required that I use a Ruby on Rails api back-end with a React front-end. The api was to be lightweight, and essentially act as a vending machine of information. This was straight-forward enough with the 
```
 rails new my_api --api
```
command. With the api format, I then used the scaffold generator to create my models. Usually scaffold is frowned upon as it can create way more code than is necessary, but in an api it only creates the controller, model, and migration file for that object.

The only thing left to do with this api was to include user authentication. You can't go up to a vending machine, press a few buttons and immediately enjoy a twix bar. You have to authenticate that transaction with your money. For this api to act similarly, I needed to include some verification in my front-end fetch requests. 

The knock gem creates a controller with a create action and a Knock::Authenticable module with an authenticate_user function. When a user logs in, they are sent to the user_token#create action that checks existing users in the database. If that user exists, it responds with a JavaScript Web Token ( jwt ) that will be stored by the front end as a cookie. When the front end sends a fetch request, it accesses the localStorage cookie for the jwt and includes it in the request. The back end api then compares the requested jwt to its own and responds accordingly. 

The issues with Knock arise in newer versions of Ruby on Rails, as it is not being kept up to date. While using Rails 5.2., I got the error 
```
TypeError (no implicit conversion of nil into String):
```

[This stack overflow link](http://stackoverflow.com/questions/49980389/rails-5-and-knock-gem-cant-authenticate-users) had the solution. A line in the config/initializers/knock.rb file has to be changed to
```
config.token_secret_signature_key = -> { Rails.application.secrets.secret_key_base }
```

In the Knock source code, it is trying to config.token_secret_signature_key to a string, which has been changed to the above location. 

This single change worked until I deployed my app to Heroku. When running the app locally it worked, but on Heroku I would get that same TypeError that I got before. After a while of searching, I found [this github thread](http://github.com/nsarno/knock/issues/205) that suggested to change that same line again to 

```
config.token_secret_signature_key = -> { Rails.application.credentials.read }
```

I'm not exactly sure why this line needed to be changed twice as I assume I am running the same version of Rails on Heroku as I was locally, but I will definitely look to use auth0 or something similar in the future instead.
