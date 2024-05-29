---
title: ''
---
# Welcome to {{site.title}} 

Welcome to my site! Here I share my ideas around topics I'm interested in, which is mainly robotics learning or tech&science related.

I'll probably end-up sharing stuff I'm probably wrong about here. The intention is to get feedback from people to improve on my thought process. Be easy on me, most of my thoughts are [open to be convinced otherwise](https://commoncog.com/strong-opinions-weakly-held-is-bad/) with a [nuanced good-faith communication](https://www.lesswrong.com/posts/wmvCcQD4naApTvrFY/guidelines-for-productive-discussions). Which I don't think is possible in most short-form web-forum style communication platforms. So feel free to reach out to me in long-form if you have some interesting points to share. (Github Issues could be fun!)


I'll think about a better blog layout after I've actually got something worth sharing published! I don't intend to publish stuff on regular basis though.



# Links to post
{% assign everything = site.posts | concat: site.projects | sort: 'date' | reverse %}

{% for post in everything limit:5 %}
## [{{post.date | date_to_string}}: {{post.title}} ]({{post.url}})
{{post.excerpt | remove_first:post.title }}
{% endfor %}


