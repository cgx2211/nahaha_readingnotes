---
layout: page
title: 心理学
showList: true
---
{% for post in site.categories.psychology %}
  [{{post.title}}]({{post.url | prepend: site.baseurl}})
{% endfor %}
