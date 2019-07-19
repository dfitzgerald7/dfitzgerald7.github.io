---
layout: post
title:      "Adding CSS to my Django Project"
date:       2019-07-15 13:05:40 -0400
permalink:  adding_css_to_my_django_project
---


This will be a short blog that just demonstrates how to add a static css file to a Django project. I used [this stack overflow](https://stackoverflow.com/questions/15491727/include-css-and-javascript-in-my-django-template/15491810) thread along with my previous JavaScript infrastructure. From my JS work, I had already added this necessary bit to settings.py
```
BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.9/howto/static-files/
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')

STATIC_URL = '/static/'

# Extra places for collectstatic to find static files.
STATICFILES_DIRS = (
    os.path.join(BASE_DIR, 'static'),
)
```
After that the static path is set up, all you need to do is actually load it in your HTML.
I added this in my main HTML file. This both loads my JS and CSS to every HTML page. Now that this is set up, I can simply add my css.
```
#notLoggedIn {
    text-align: center;
}

.main-container {
    width: 800px;
    margin-left: auto;
    margin-right: auto;
}

#addLabBtn {
    text-align: center;
}
```
