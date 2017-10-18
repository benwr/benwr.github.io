---
layout: page
---
### Unpublished Posts

Congratulations, you've found my collection of unpublished
posts, which I use to share with people to whom I give the link.

This content is unpublished for a reason, and that reason is mostly
that I don't think it's very good (yet). Accordingly, please refrain
from sharing it. If I find that people know about this page, I'll
probably have to stop using it.

{% for post in site.categories['unpublished'] %}
* [{{ post.title }}]({{ post.url }}) ({{ post.date | date: '%B %d, %Y' }}) {% endfor %}