---
title: ''
---

{% assign everything = site.posts | concat: site.projects | sort: 'date' | reverse %}

{% for post in everything %}
#### [{{post.title}}]({{post.url}})
>[{{post.date | date_to_string}} : {{post.tldr | remove_first:post.title }}]({{post.url}})
{% endfor %}


