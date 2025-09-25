---
title: Dokumentation
layout: default
---

{% assign docs = site.pages
  | where_exp: "p", "p.path contains 'docs/'"
  | where_exp: "p", "p.url != page.url"
  | sort: "title" %}
<ul>
  {% for p in pages %}
    <li><a href="{{ p.url | relative_url }}">{{ p.title | default: p.name }}</a></li>
  {% endfor %}
</ul>
