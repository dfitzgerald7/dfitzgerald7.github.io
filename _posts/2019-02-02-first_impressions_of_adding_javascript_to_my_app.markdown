---
layout: post
title:      "First impressions of Adding JavaScript to my App. "
date:       2019-02-02 19:04:28 +0000
permalink:  first_impressions_of_adding_javascript_to_my_app
---

After fumbling around with the hoistings and the weird scopes of the JavaScript world, I now understand why its integral to web design. It can make a web page feel much more than just a static object to be read. For my fourth project, I added a JavaScript front end to my Ruby on Rails restaurant review app. 

The project essentially replaced some RESTful Ruby actions of the app with JavaScript. The first thing I noticed when working was how it would cut down the amount of pages in my app. Right now, the app only has two main pages while still rendering an index page, two show pages, and a create form.  The app feels more accessible since most of the information is right there, but not all at once. The user has access to much more info immediately but can choose what they want to display. 

The hardest part for me about this project was getting my rendered form to work properly. I wanted to have a button on the root page that would render a form to submit a new review. Once clicked, the form would be rendered at the top of the page. If the input was invalid, nothing would happen except for an alert message. If valid, the new review would be prepended to the reviews div and the form would be hidden, awaiting the new review button to be clicked again. The biggest issue revolved around multiple submissions without a page refresh. The submit button would disable itself after a valid submission. After some googling, I found a property method that would allow me to call prop("disabled", false) to be called on the submit button.
