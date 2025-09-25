{% assign docs = site.pages
  | where_exp: "p", "p.path contains 'docs/'"
  | where_exp: "p", "p.url != page.url"
  | sort: "title" %}
<ul>
  {% for p in docs %}
    <li><a href="{{ p.url | relative_url }}">{{ p.title | default: p.name }}</a></li>
  {% endfor %}
</ul>


---
date: 2024-12-19
---

# Index

Im Folgenden eine Sammlung von Gedanken, die ich irgendwo gehört, gelesen oder selbst gedacht habe und die ich für wertvoll halte, um sie festzuhalten.

- [Es aushalten - Eigentliche Resilienz](./pages/001_es-aushalten-eigentliche-resilienz.md)
- [Fokussierung](./pages/002_fokussierung.md)
- [Glauben - Meinen - Wissen](./pages/003_glauben-meinen-wissen.md)
- [Woher kommt Motivation](./pages/004_motivation-vom-handlen.md)
- [Prokrastination](./pages/005_prokrastination.md)
- [Selbstwirksamkeit](./pages/006_selbstwirksamkeit.md)
- [Behavioural Activation](./pages/007_behavioural-activation.md)
- [Teile und Herrsche](./pages/008_teile-und-hersche.md)
- [Kern der Sache](./pages/009_kern-der-sache.md)
- [Sei nicht so wichtig](./pages/010_sei-nicht-so-wichtig.md)
- [GRIT](./pages/011_grit.md)
- [Clustern](./pages/012_clustern.md)
- [Yes or No](./pages/013_yes-or-no.md)
- [Meinungen biegen](./pages/014_meinungen-biegen.md)
- [Viewpoint flattening](./pages/015_viewpoint-view-flattening.md)
- [Kaizen - Continuous Improvement](./pages/016_kaizen.md)
- [Plan with your Obstacles](./pages/017_plan-with-your-obstacles.md)
- [Schnell reagieren](./pages/018_schnell-reagieren.md)
- [Wieviel Zeit investieren](./pages/019-wieviel-zeit-investieren.md)
- [Asking / Fragen](./pages/020_asking.md)
- [Wie entsteht Geld](./pages/021_wie-entsteht-geld.md)
- [Stress](./pages/022-stress.md)
- [Gut gemeint](./pages/023_gut-gemeint.md)
- [Art und Weise](./pages/024_die-art-und-weise.md)
- [Rezession, Inflation, Konjunktur](./pages/025-rezession-inflation-konjunktur.md)
- [Wut](./pages/026-wut.md)
- [Mitten im Feuer](./pages/027-mitten-im-feuer.md)
