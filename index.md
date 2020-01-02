---
layout: default
title: "toboto Blog"
---

## 近期文章
{% for post in site.posts %}
### [{{ post.title }}]({{ post.url }})
> {{ post.excerpt}}

<p class="post-meta">
Posted by {% if post.author %}{{ post.author }}{% else %}{{ site.title }}{% endif %} on {{ post.date | date: "%B %-d, %Y" }}
</p>
{% endfor %}

