---
layout  : page
title   : Tags
---
<ul class="tag-cloud">
{% assign sorted_tags = (site.tags | sort: 0) %}
{% for tag in sorted_tags %}
    <a href="/tags/{{ tag[0] }}">
      {{ tag | first }} ({{ tag | last | size }})
    </a>
{% endfor %}
</ul>
