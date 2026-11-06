---
layout: page
permalink: /talks/
title: talks
nav: true
nav_order: 7
---

{% assign talks = site.data.talks.talks %}
<ol class="talks-list">
{% for talk in talks %}
  <li>
    <a href="{{ talk.permalink | relative_url }}">{{ talk.title }}</a>
  </li>
{% endfor %}
</ol>
