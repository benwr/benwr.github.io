---
layout: page
---
### Notes

{% for post in site.categories['notes'] %}
* [{{ post.title }}]({{ post.url }}) ({{ post.date | date: '%B %d, %Y' }}) {% endfor %}