---
layout: page
title: 经济
permalink: /economicwayofthinking/
---
{% for post in site.categories.economic %}
  <a href="{{post.url | prepend: site.baseurl}}">{{post.title}}</a>
{% endfor %}
