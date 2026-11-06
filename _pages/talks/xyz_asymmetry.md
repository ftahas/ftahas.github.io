---
layout: page
permalink: /talks/xyz-asymmetry/
title: Entanglement asymmetry in the gapped XYZ spin-1/2 chain
description: A four-part animated presentation, playable in the browser
nav: false
---

[&larr; all talks]({{ '/talks/' | relative_url }})

A four-part animated presentation of my paper [Entanglement asymmetry in the gapped XYZ spin-1/2 chain](https://arxiv.org/abs/2607.25625), written for undergraduates who know linear algebra, probability and introductory quantum mechanics. The presentation is conceptual and analytical: formulas and pictures, no numerical results. Each part is a 20-25 minute live session. The animations were built with [Manim](https://www.manim.community/) and exported with [manim-slides](https://manim-slides.eertmans.be/); the slides play in the browser, no download needed.

**How to drive a deck.** Click a part below: the first clip starts on its own. The right arrow (or `n`) plays the next stop, the left arrow replays the previous one, and space pauses or resumes the current clip. Press `f` for fullscreen, `o` for an overview of all stops, `s` for the speaker notes and `?` for every key. The clips are silent: the narration is spoken live, so the notes carry the cue sheet. The handout of each part has one page per stop, the last frame of each clip.

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
