---
title: Dokumentation
layout: default
---

{% assign docs = site.pages
  | where_exp: "p", "p.path contains 'pages/'"
  | where_exp: "p", "p.url != page.url"   /* sich selbst ausschließen */
  | sort: "title" %}
<ul>
{% for p in docs %}
  <li><a href="{{ p.url | relative_url }}">{{ p.title | default: p.name }}</a></li>
{% endfor %}
</ul>
