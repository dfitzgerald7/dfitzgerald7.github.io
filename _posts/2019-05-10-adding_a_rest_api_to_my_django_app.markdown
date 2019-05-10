---
layout: post
title:      "Adding a REST API to my Django app"
date:       2019-05-10 19:49:55 +0000
permalink:  adding_a_rest_api_to_my_django_app
---


After showing my first Django app to a developer, he recommended that I [this api framework](https://www.django-rest-framework.org//). It is middleware that sits on top of the database. Instead of directly interacting with the database, the front end will make calls to an API that returns serialized versions of the models. Since the front end doesn't have to directly interact with the data, the database itself can be more easily changed. 

The set up has been relatively painless so far. After following the directions on the website and installing the packages, I took to youtube and found this [video](https://www.youtube.com/watch?v=263xt_4mBNc&t=1262s). The steps layed out are 

1. Install packages
2. Add apps in settings 
3. Create your models 
4. Create your serializers, a class for each model that inherits from the serializers module from rest_framework
5. Use the register method in the urls file to create all restful routes for the model

With all of that set up, the app now has end points for all crud actions. What this video does not cover and what I am still trying to figure out is how to implement this in my sample app. Questions like where in my app to send fetch requests still need answers. 
