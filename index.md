---
title: Übersicht
layout: default
---

{%- comment -%}
1) Kandidaten einschränken:
   - nur Dateien unter /pages/
   - nur Markdown
   - nicht die aktuelle Seite
{%- endcomment -%}
{% assign candidates = site.pages
  | where_exp: "p", "p.path contains '/pages/'"
  | where_exp: "p", "p.extname == '.md' or p.extname == '.markdown'"
  | where_exp: "p", "p.url != page.url" %}

{%- comment -%}
2) Nach URL deduplizieren
{%- endcomment -%}
{% assign groups = candidates | group_by: "url" %}
{% assign pages = "" | split: "" %}
{% for g in groups %}
  {% assign pages = pages | push: g.items.first %}
{% endfor %}

{%- comment -%}
3) Sortieren (optional: nach URL)
{%- endcomment -%}
{% assign pages = pages | sort: "url" %}

<ul>
{%- for p in pages -%}
  {%- assign label = p.title | to_s | strip -%}

  {%- if label == "" -%}
    {%- assign html = p.content | markdownify -%}
    {%- if html contains "<h1>" -%}
      {%- assign label = html
         | split: "<h1>" | slice: 1, 1 | first
         | split: "</h1>" | first
         | strip_html | strip -%}
    {%- endif -%}
  {%- endif -%}

  {%- assign label = label | default: p.name | strip -%}

  <li><a href="{{ p.url | relative_url }}">{{ label }}</a></li>
{%- endfor -%}
</ul>
