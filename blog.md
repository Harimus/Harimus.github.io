---
title: ''
---
{% assign everything = site.posts  | sort: 'date' | reverse %}

{% for post in everything %}
#### [{{post.title}}]({{post.url}})
>[{{post.date | date_to_string}} : {{post.tldr | remove_first:post.title }}]({{post.url}})
{% endfor %}


