---
title: Home
layout: home
---

I'm Alexander Shlyapin and this is my personal wiki.

<ul>
{% for page in site.pages %}
  {% if page.title %}
    <li><a href="{{ page.url | relative_url }}">{{ page.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>

