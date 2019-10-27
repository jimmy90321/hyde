---
layout  : page
title   : Tags
---
<ul class="tag-cloud">
{% assign sorted_tags = site.tags %}
{% for tag in sorted_tags %}
  <li>
    <a href="/tags/{{ tag[0] }}">
      {{ tag | first }} ({{ tag | last | size }})
    </a>
  </li>
{% endfor %}
</ul>
