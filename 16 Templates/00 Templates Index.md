---
title: Templates Index
aliases:
  - Templates
  - Templates Index
domain: Templates
module: Index
status: Learning
difficulty: Easy
priority: Medium
interview: 1
revision: Monthly
order: 0
tags:
  - templates
  - index
---

# Templates

> Reusable note templates. Copy one when creating a new note so every note starts with the standard frontmatter and structure.

## Available Templates
1. [[Technology Template]] — for a technical concept (the default for most notes).
2. [[System Design Template]] — for a system-design case study.
3. [[Interview Template]] — for a Q&A / interview-question note.
4. [[Project Template]] — for a hands-on project.
5. [[Daily Learning Template]] — for a daily study log.
6. [[Revision Template]] — for a revision/cheat-sheet note.

## Standard Frontmatter
Every note should carry these properties (see [[Properties Guide]] for allowed values):

```yaml
---
title: 
aliases: []
domain: 
module: 
status: Not Started      # Not Started | Learning | Completed | Need Revision
difficulty: Medium       # Easy | Medium | Hard
priority: Medium         # High | Medium | Low
interview: 3             # 1-5
revision: Weekly         # Daily | Weekly | Monthly
order: 0
tags: []
related: []
---
```

## How to Use
- With the core **Templates** plugin: set this folder as the template folder, then "Insert template".
- Or copy a template's contents into a new note and fill the placeholders.
- Keep numbered filenames (`NN Topic.md`) inside module folders so ordering and the bases stay correct.

## Topic Tracker

> Live, auto-updating table of every note in this domain, grouped by module.

![[Templates.base]]
