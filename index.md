---
title: Übersicht
layout: default
---

<h1>{{ page.title }}</h1>

{%- comment -%}
1) Kandidaten: nur Dateien in pages/, nicht die aktuelle Seite
   (Achtung: ohne führenden Slash filtern!)
{%- endcomment -%}
{% assign candidates = site.pages
  | where_exp: "p", "p.path contains 'pages/'"
  | where_exp: "p", "p.url != page.url" %}

{%- comment -%}
2) Nach URL deduplizieren und nach URL sortieren
{%- endcomment -%}
{% assign groups = candidates | group_by: "url" | sort: "name" %}

<ul>
{%- for g in groups -%}
  {%- assign p = g.items.first -%}
  {%- unless p.path contains 'target-repo/' -%}
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
  {%- endunless -%}
{%- endfor -%}
</ul>
