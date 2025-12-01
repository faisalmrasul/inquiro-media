---
layout: page
title: "Post Archive"
permalink: /archive/
---

# Complete Archive

All posts in chronological order:

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url | prepend: site.baseurl }}) - {{ post.date | date: "%B %d, %Y" }}
{% endfor %}

**Total Posts:** {{ site.posts | size }}
