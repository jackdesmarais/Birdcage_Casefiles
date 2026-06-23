---
layout: default
---

{{ content }}

{% capture faction_content %}
{% assign faction_npcs = "" | split: "" %}
{% assign faction_pcs = "" | split: "" %}

{% comment %} Find NPCs in this faction {% endcomment %}
{% for npc in site.NPCs %}
  {% if npc.faction contains page.title %}
    {% assign faction_npcs = faction_npcs | push: npc.title %}
  {% endif %}
{% endfor %}

{% comment %} Find PCs in this faction {% endcomment %}
{% for pc in site.PCs %}
  {% if pc.faction contains page.title %}
    {% assign faction_pcs = faction_pcs | push: pc.title %}
  {% endif %}
{% endfor %}

{% assign unique_npcs = faction_npcs | uniq | sort %}
{% if unique_npcs.size > 0 %}
## NPC Members
{% for npc in unique_npcs %}
- [{{ npc }}](/Birdcage_Casefiles/NPCs/{{ npc | replace: " ", "_" }}.html)
{% endfor %}
{% endif %}

{% assign unique_pcs = faction_pcs | uniq | sort %}
{% if unique_pcs.size > 0 %}
## PC Members
{% for pc in unique_pcs %}
- [{{ pc }}](/Birdcage_Casefiles/PCs/{{ pc | replace: " ", "_" }}.html)
{% endfor %}
{% endif %}

{% comment %} Find sessions mentioning this faction {% endcomment %}
{% assign session_notes = site.session_notes | where_exp: "note", "note.content contains page.title" %}
{% if session_notes.size > 0 %}
## Sessions appearing
{% for note in session_notes %}
{% assign hierarchy = note.title %}
{% if note.parent %}
  {% assign hierarchy = note.parent | append: " - " | append: hierarchy %}
  {% assign parent_page = site.session_notes | where: "title", note.parent | first %}
  {% if parent_page.parent %}
    {% assign hierarchy = parent_page.parent | append: " - " | append: hierarchy %}
  {% endif %}
{% endif %}
{% assign path_parts = note.path | split: "/" %}
{% assign dir_path = path_parts | slice: 1, path_parts.size | join: "/" | remove: ".md" %}

- [{{ hierarchy }}](/Birdcage_Casefiles/session_notes/{{ dir_path }}.html)
{% endfor %}
{% endif %}
{% endcapture %}

{{ faction_content | markdownify }}
