# Welcome to {{site.title}} 

Welcome to my blog Wrong Today! I'll share stuff I'm probably wrong about here,
so that people can point out how wrong I am today, so I can correct myself tomorrow.

I'll think about a better blog layout after I've actually got something worth sharing published!




# Links to post
{% assign everything = site.posts | concat: site.projects | sort: 'date' | reverse %}

{% for post in everything limit:5 %}
## [{{post.date | date_to_string}}: {{post.title}} ]({{post.url}})
{{post.excerpt}}
{% endfor %}


