# Birdcage Casefiles

A Jekyll-powered campaign wiki for a multi-system game set in The Birdcage, viewable at [jackdesmarais.github.io/Birdcage_Casefiles](https://jackdesmarais.github.io/Birdcage_Casefiles).

## Overview
This is a living case file document for a shared setting visited by time travelers, secret operatives, and boy scouts on merit badge missions. Multiple organizations — the City Living History Association, Troop 27756, and Delta Green — send agents into the Birdcage's timeline to nudge, correct, or confront what they find there.

## Website Structure

### Collections
- `_session_notes/`: Campaign session summaries, organized by arc and organization
- `_NPCs/`: NPC character pages
- `_PCs/`: Player character pages
- `_locations/`: Location descriptions
- `_factions/`: Organization descriptions
- `_items/`: Items and artifacts

### Automated Features
The site uses custom layouts to automatically maintain relationships between pages:

- `_layouts/NPC.md`: Shows sessions where an NPC appears, based on session note content
- `_layouts/PC.md`: Shows sessions a PC appears in, based on session note front matter
- `_layouts/location.md`: Lists sessions mentioning the location, based on session note content
- `_layouts/faction.md`: Shows NPC and PC members, plus sessions mentioning the faction

### Session Notes Format
Session notes use YAML front matter to track player characters present and the parent arc structure.

Example:
```yaml
---
title: Session Name
layout: default
parent: Arc Name
players:
- name: Player Name
  character: Character Name
date: YYYY-MM-DD
---
```

### PC Front Matter
PC front matter tracks the player, status, and any aliases (callsigns, codenames).
```yaml
---
title: Character Name
layout: PC
player: Player Name
status: Active
aliases:
  - CALLSIGN
---
```

## Systems
- [FATE Core](https://fate-srd.com/fate-core) — used for CLHA and Troop 27756 operations
- [Delta Green](https://deltagreengame.com/) — used for present-day operations
