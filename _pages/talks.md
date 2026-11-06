---
layout: page
permalink: /talks/
title: talks
description: Animated presentations of my work, playable in the browser
nav: true
nav_order: 7
---

Each talk below has its own page with the slides, which play directly in the browser, and a handout.

{% assign talks = site.data.talks.talks %}
<ol class="talks-list">
{% for talk in talks %}
  <li>
    <a href="{{ talk.permalink | relative_url }}">{{ talk.title }}</a>
    <br><small class="text-muted">{{ talk.blurb }}</small>
  </li>
{% endfor %}
</ol>
