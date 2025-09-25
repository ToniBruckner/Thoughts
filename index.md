---
title: Übersicht
layout: default
---

<h1>{{ page.title }}</h1>

{%- comment -%}
1) Kandidaten: nur Dateien in pages/, nicht die aktuelle Seite
   (ohne führenden Slash filtern!)
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

      {%- comment -%} H1 extrahieren – tolerant gegenüber Attributen in <h1 ...>{%- endcomment -%}
      {%- assign parts = html | split: '<h1' -%}
      {%- if parts.size > 1 -%}
        {%- assign after_open = parts[1] | split: '>' | slice: 1, 1 | first -%}
        {%- assign label = after_open | split: '</h1>' | first | strip_html | strip -%}
      {%- else -%}
        {%- comment -%} Optionaler Fallback: H2, falls keine H1 vorhanden {%- endcomment -%}
        {%- assign parts2 = html | split: '<h2' -%}
        {%- if parts2.size > 1 -%}
          {%- assign after_open2 = parts2[1] | split: '>' | slice: 1, 1 | first -%}
          {%- assign label = after_open2 | split: '</h2>' | first | strip_html | strip -%}
        {%- endif -%}
      {%- endif -%}
    {%- endif -%}

    {%- assign label = label | default: p.name | strip -%}

    <li><a href="{{ p.url | relative_url }}">{{ label }}</a></li>
  {%- endunless -%}
{%- endfor -%}
</ul>
