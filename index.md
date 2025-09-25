---
title: Übersicht
layout: default
---

{% assign urls = site.pages
  | where_exp: "p", "p.path contains 'pages/'"
  | where_exp: "p", "p.url != page.url"
  | map: "url"
  | uniq
  | sort %}

<ul>
{% for u in urls %}
  {% assign p = site.pages | where: "url", u | first %}
  <li><a href="{{ p.url | relative_url }}">{{ p.title | default: p.name }}</a></li>
{% endfor %}
</ul>
