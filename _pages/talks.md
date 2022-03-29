---
title: Talks
layout: default
permalink: /talks/
published: true
---

{% for talk in site.talks %}
  <article class="talk">
    <h2>{{ talk.title }}</h2>
    <time datetime="{{ talk.date | date_to_xmlschema }}">{{ talk.date | date: '%B %Y' }}</time>
    <h3>{{ talk.event }}</h3>
    <p>{{ talk.content }}</p>
  {% if talk.video %}
    <i class="fas fa-video"></i> <a href="{{ talk.video }}">Video</a>
  {% endif %}
  {% if talk.slides %}
    <i class="fas fa-person-chalkboard"></i> <a href="{{ talk.slides }}">Slides</a>
  {% endif %}
  {% if talk.site %}
    <i class="fas fa-globe"></i> <a href="{{ talk.site }}">Site</a>
  {% endif %}
  </article>
{% endfor %}
