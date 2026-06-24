---
layout: default
---

{% if page.status %}
{% capture status_block %}
> **Status:** {{ page.status }}
{% endcapture %}
{{ status_block | markdownify }}
{% endif %}

{{ content }}

{% capture pc_content %}
{% assign session_notes = site.session_notes | where_exp: "note", "note.players" %}
{% assign matching_notes = "" | split: "" %}
{% for note in session_notes %}
  {% for player in note.players %}
    {% if player.character == page.title %}
      {% assign matching_notes = matching_notes | push: note %}
      {% break %}
    {% endif %}
  {% endfor %}
{% endfor %}

{% if matching_notes.size > 0 %}
## Sessions appearing
{% for note in matching_notes %}
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

{{ pc_content | markdownify }}
