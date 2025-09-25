---
title: Übersicht
layout: default
---

{% assign pages = site.pages
  | where_exp: "p", "p.path contains 'pages/'"
  | where_exp: "p", "p.url != page.url"
  | sort: "url" %}

<ul>
{% for p in pages %}
  {% assign label = p.title | to_s %}

  {% if label == "" %}
    {% assign html = p.content | markdownify %}
    {% if html contains "<h1>" %}
      {% assign label = html | split: "<h1>" | last | split: "</h1>" | first | strip_html | strip %}
    {% elsif html contains "<h2>" %}
      {% assign label = html | split: "<h2>" | last | split: "</h2>" | first | strip_html | strip %}
    {% endif %}
  {% endif %}

  {% assign label = label | default: p.name %}

  <li>
    <a href="{{ p.url | relative_url }}">{{ label }}</a>
  </li>
{% endfor %}
</ul>
