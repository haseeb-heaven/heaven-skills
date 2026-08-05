---
name: obsidian-vault
description: >-
  Search, create, and manage Obsidian vault notes programmatically. Covers note creation
  with YAML frontmatter, backlink management, graph analysis, tag organization, template
  usage, and plugin integration. Use when automating note-taking workflows, building
  knowledge management systems, or querying vault content from scripts.
version: 1
---

# Obsidian Vault

Search, create, and manage Obsidian vault notes for personal knowledge management.

## When NOT to Use

- Large document databases (use Elasticsearch, Notion API, or Confluence)
- Real-time collaborative editing — use Google Docs or Notion instead
- Structured data with complex relationships — use a proper database

## Core Concepts

| Concept | Description | Example |
|---------|-------------|---------|
| **Note** | A single markdown file (.md) in the vault | `2024-01-15-meeting-notes.md` |
| **Backlink** | Link from one note to another using `[[wikilinks]]` | `See [[Project Alpha]]` |
| **Tag** | Hierarchical metadata prefix with `#` | `#projects/alpha`, `#meetings` |
| **Frontmatter** | YAML metadata at top of note | `tags: [project, meeting]` |
| **Daily Note** | Auto-created daily journal entry | `2024-01-15.md` |
| **Folder** | Directory organizing notes by context | `Projects/`, `Inbox/` |

## Common Operations

### Creating a Note
```yaml
---
title: "Note Title"
created: 2024-01-15
tags: [tag1, tag2]
type: [[Type]]
---

# Note Title

Content goes here...
```

### Searching Notes
```bash
# By filename
grep -ril "search term" ~/Vault/

# By tags
grep -rl "^tags:.*target-tag" ~/Vault/

# By date range
find ~/Vault/ -name "2024-*" -type f

# By frontmatter field
grep -rl "status: active" ~/Vault/
```

### Managing Backlinks
Backlinks are automatically tracked by Obsidian. To find links pointing to a note:
```bash
# Find all notes that link to this one
grep -rl "\[\[TargetNote\]\]" ~/Vault/
```

### Tag Patterns

| Pattern | Purpose | Example |
|---------|---------|---------|
| Flat tags | Simple categorization | `#idea`, `#todo`, `#done` |
| Namespace tags | Group related categories | `#project/alpha`, `#project/beta` |
| Type tags | Classify note format | `#meeting`, `#reference`, `#journal` |
| Status tags | Track progress | `#wip`, `#review`, `#archived` |

## Template Examples

### Meeting Notes Template
```markdown
---
title: "{{title}}"
date: {{date}}
tags: [meeting, {{type}}]
attendees: []
---

# {{title}}

## Agenda
1. 

## Notes


## Action Items
- [ ] 

## Related
- [[Link to related project]]
```

### Project Tracker Template
```markdown
---
title: "{{title}}"
status: planning
priority: medium
created: {{date}}
tags: [project]
---

# {{title}}

## Overview


## Goals
- [ ] Goal 1
- [ ] Goal 2

## Timeline
- Planning: TBD
- Development: TBD
- Launch: TBD

## Resources
- [[Related note]]

## Progress


## Archive
_When complete, move this note to `Archive/projects/` folder_
```

## Plugin Integration

### Useful Plugins for Automation

| Plugin | Purpose | Automation Value |
|--------|---------|-----------------|
| **Templater** | Advanced templates with JS | Dynamic note generation |
| **QuickAdd** | Capture snippets quickly | Bulk note creation |
| **Dataview** | Query notes as tables | Knowledge base dashboards |
| **Obsidian Git** | Version control vault | Track note history |
| **Tasks** | Cross-note task management | Automated action tracking |

## Best Practices

1. **One idea per note** — Easier to link, search, and reuse than mega-documents
2. **Use consistent naming** — `YYYY-MM-DD-topic` for time-based, `topic-subtopic` for concepts
3. **Tag hierarchically** — `#area/project/topic` enables both broad and narrow filtering
4. **Link liberally** — More connections = richer graph navigation
5. **Review weekly** — Clean up inbox folder, archive completed items, update status tags
