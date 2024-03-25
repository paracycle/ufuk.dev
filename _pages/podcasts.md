---
title: Podcasts
layout: default
permalink: /podcasts/
published: true
---

{% for podcast in site.podcasts reversed %}
  <article class="talk">
    <h2>{{ podcast.title }}</h2>
    <time datetime="{{ talk.date | date_to_xmlschema }}">
      {% if podcast.episode %}
        Episode {{ podcast.episode }} -
      {% endif %}
      {{ podcast.date | date: '%B %Y' }}
    </time>
    <h3>
      {{ podcast.podcast }}
    </h3>
    {{ podcast.content }}
    <p class="footer">
    {% if podcast.link %}
      <i class="fas fa-microphone"></i>
      <a href="{{ podcast.link }}">Listen</a>
    {% endif %}
    {% if podcast.video %}
      <i class="fas fa-video"></i>
      <a href="{{ podcast.video }}">Watch</a>
    {% endif %}
    </p>
  </article>
{% endfor %}
