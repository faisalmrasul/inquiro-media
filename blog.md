---
layout: page
title: "Blog Archive"
permalink: /blog/
---

# All Blog Posts

Browse all articles published on Inquiro Media.

{% for post in site.posts %}
## [{{ post.title }}]({{ post.url | prepend: site.baseurl }})
*{{ post.date | date: "%B %d, %Y" }} • {{ post.categories | join: ", " }}*

{% if post.excerpt %}
{{ post.excerpt }}
{% endif %}

[Read More →]({{ post.url | prepend: site.baseurl }})
<hr>
{% endfor %}

## Categories
{% assign categories = site.posts | map: 'categories' | flatten | uniq %}
{% for category in categories %}
- [{{ category }}](/category/{{ category | slugify }})
{% endfor %}
