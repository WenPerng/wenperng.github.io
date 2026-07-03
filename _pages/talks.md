---
layout: page
title: talks
permalink: /talks/
description: A list of talks that I have given throughout the years.
nav: true
nav_order: 3
display_categories: [IPhOC, NTUEE SAAD]
horizontal: false
---

<!-- pages/talks.md -->
<div class="projects">
{% if site.enable_talk_categories and page.display_categories %}
  <!-- Display categorized talks -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_talks = site.talks | where: "category", category %}
  {% assign sorted_talks = categorized_talks | sort: "date" | reverse %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_talks %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_talks %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_talks = site.talks | sort: "date" | reverse %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for talk in sorted_talks %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for talk in sorted_talks %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>
