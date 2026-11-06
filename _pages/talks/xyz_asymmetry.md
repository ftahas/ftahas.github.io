---
layout: page
permalink: /talks/xyz-asymmetry/
title: Entanglement asymmetry in the gapped XYZ spin-1/2 chain
nav: false
---

[&larr; all talks]({{ '/talks/' | relative_url }})

{% assign talks_root = '/assets/talks/xyz-asymmetry' %}

<div class="row row-cols-1 row-cols-md-2 mt-4">
{% assign parts = site.data.talks.xyz_asymmetry %}
{% for part in parts %}
  <div class="col mb-4">
    <div class="card h-100">
      <a href="{{ talks_root | append: '/' | append: part.folder | append: '/' | relative_url }}" target="_blank" rel="noopener">
        <img src="{{ talks_root | append: '/' | append: part.folder | append: '/poster.png' | relative_url }}" class="card-img-top" alt="First frame of {{ part.title }}" loading="lazy">
      </a>
      <div class="card-body">
        <h5 class="card-title">Part {{ part.number }}: {{ part.title }}</h5>
        <p class="card-text">{{ part.summary }}</p>
        <p class="card-text"><small class="text-muted">{{ part.scenes }} scenes, {{ part.stops }} stops, {{ part.minutes }} min of animation</small></p>
        <a href="{{ talks_root | append: '/' | append: part.folder | append: '/' | relative_url }}" class="btn btn-sm z-depth-0" role="button" target="_blank" rel="noopener">&#9654;&nbsp; Play in the browser</a>
        <a href="{{ talks_root | append: '/' | append: part.folder | append: '/handout.pdf' | relative_url }}" class="btn btn-sm z-depth-0" role="button" target="_blank" rel="noopener">Handout (PDF)</a>
      </div>
    </div>
  </div>
{% endfor %}
</div>
