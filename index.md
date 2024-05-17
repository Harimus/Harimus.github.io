---
title: ''
---
# Welcome to {{site.title}} 

Welcome to my blog! Here I share my ideas around topics I'm interested in, which is mainly robotics.

I'll probably end-up sharing stuff I'm probably wrong about here. The intention is to get feedback from people to improve on my thought process.


I'll think about a better blog layout after I've actually got something worth sharing published!




# Links to post
{% assign everything = site.posts | concat: site.projects | sort: 'date' | reverse %}

{% for post in everything limit:5 %}
## [{{post.date | date_to_string}}: {{post.title}} ]({{post.url}})
{{post.excerpt | remove_first:post.title }}
{% endfor %}


