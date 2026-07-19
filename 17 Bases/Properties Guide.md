---
title: Properties Guide
aliases:
  - Properties Guide
domain: Bases
module: 
status: Learning
difficulty: Easy
priority: Medium
interview: 1
revision: Monthly
order: 1
tags:
  - bases
---

# Properties Guide

> The standard frontmatter schema every note uses. Bases read these properties for columns, filters, and sorting.

## Schema
```yaml
---
title:               # display title (usually the note name)
aliases: []          # clean-name aliases so wiki links resolve despite NN prefixes
domain:              # top-level domain (Java, Spring, ...)
module:              # the module folder the note lives in
status: Not Started  # Not Started | Learning | Completed | Need Revision
difficulty: Medium   # Easy | Medium | Hard
priority: Medium     # High | Medium | Low
interview: 3         # 1-5 (interview importance)
revision: Weekly     # Daily | Weekly | Monthly
order: 0             # position within the module (drives sorting)
tags: []             # lowercase, kebab-case
related: []          # list of related notes as wiki links
---
```

## Allowed Values
| Property | Values |
|----------|--------|
| status | Not Started, Learning, Completed, Need Revision |
| difficulty | Easy, Medium, Hard |
| priority | High, Medium, Low |
| interview | 1, 2, 3, 4, 5 |
| revision | Daily, Weekly, Monthly |
| order | integer (module reading order) |

## Conventions
- Keep property **names** lowercase.
- `interview` is a number (1-5), not `true/false` — enables sorting the Interview Dashboard.
- `order` mirrors the note's `NN` filename prefix within its module.
- `domain` matches the top-level folder; `module` matches the module subfolder.
- Every numbered note has an `aliases` entry equal to its clean name so wiki links keep working.

## Example Filters (Bases)
```
file.inFolder("04 Java")
note.status == "Learning"
note.interview >= 4
note.priority == "High"
```
