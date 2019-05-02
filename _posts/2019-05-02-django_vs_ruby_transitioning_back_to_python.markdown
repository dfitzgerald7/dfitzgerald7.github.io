---
layout: post
title:      "Django vs. Ruby: Transitioning back to Python"
date:       2019-05-02 21:30:41 +0000
permalink:  django_vs_ruby_transitioning_back_to_python
---


Python was my introduction into computer science. It was what I learned in my first class that I took in college. After learning a few more languages, I hadn't touched it since then. As an exercise in education and determination, I decided that I would familiarize myself with Django, the Python web framework, and get a basic app up all within a few days. It proved to be a challenging but rewarding experience. I am far from a django expert but this is my experience so far. 

The first difference proves to be rather annoying at first. Both being MVC frameworks, there are models, views, and controllers. In django, the concept is the same but there are models, views, and templates. The ruby controller is the django view and the ruby view is the django template. This difference is inconsequential once some time has passed but can take a bit to get used to.

The second difference was the importance of a virtual environment. Having used Ruby's bundler and JavaScript's npm, I had never had to think about what versions of packages I was using. The lockfiles that were created by using those package managers always took care of that. My understanding with pip, Python's package manager, is that you have to do that manually. I did not use a virtual environment for my first attempt. It worked fine until I tried to deploy it on Heroku. To deploy it I needed a requirements.txt file, which is the python equivalent of the gemfile. To create this file, I ran  

```
pip freeze > requirements.txt
```

which mapped all packages in the environment to that file. Based on the guide that I was going off there should have only been several packages but since I was not in an isolated virtual environment pip was finding much more than it should have. My solution was to create a new directory with a virtual environment, copy my code over, then pip install and freeze from that directory.

Overall, I felt that this was a great use of my time. The most important skills that I have learned thoughout my education are research and persistance. This exercise made me more confident that with my general web development knowledge and some googling that I could expand into other languages. 
