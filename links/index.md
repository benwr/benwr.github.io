---
layout: page
title: Links
---
### Links

The following is a collection of links that I thought were interesting
for one reason or another.

{% for post in site.categories['links'] %}
* [{{ post.title }}]({{ post.url }}) ({{ post.date | date: '%B %d, %Y' }}) {% endfor %}