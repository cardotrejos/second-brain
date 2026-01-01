# AGENTS.md

Instructions for Claude Code subagents working with this Obsidian vault.

## Context

This is a personal knowledge management vault using the **PARA system** (Projects, Areas, Resources, Archives) based on the Building a Second Brain methodology.

## Vault Location

```
/Users/cardotrejos/Library/Mobile Documents/iCloud~md~obsidian/Documents/Personal/
```

## PARA Folder Purposes

| Folder | Purpose | Examples |
|--------|---------|----------|
| `0 - Inbox/` | Unsorted captures, quick notes | New ideas, things to process |
| `1 - Projects/` | Active work with end goals | Courses, apps, features to ship |
| `2 - Areas/` | Ongoing responsibilities | Trading, Blog, Side business |
| `3 - Resources/` | Reference by topic | Programming languages, tools |
| `4 - Archives/` | Completed/inactive | Done projects, old resources |

## Agent Guidelines

### When Creating Notes

1. Default to `0 - Inbox/` unless destination is obvious
2. Use clear, descriptive filenames
3. Include frontmatter if the note has metadata:
   ```yaml
   ---
   created: YYYY-MM-DD
   tags: [tag1, tag2]
   ---
   ```

### When Organizing Notes

Ask these questions in order:
1. Is this tied to an active project? → `1 - Projects/{project-name}/`
2. Is this an ongoing area of life? → `2 - Areas/{area-name}/`
3. Is this reference material? → `3 - Resources/{topic}/`
4. Is this done or stale? → `4 - Archives/`

### When Searching for Content

- **Project-related:** Search in `1 - Projects/`
- **Ongoing topics:** Search in `2 - Areas/`
- **Technical reference:** Search in `3 - Resources/`
- **Historical/completed:** Search in `4 - Archives/`

### Obsidian Syntax Rules

- Use `[[Note Name]]` for internal links (not markdown links)
- Use `![[Note Name]]` to embed content
- Use `#tags` for categorization
- Preserve existing wikilinks when editing

### Current Projects (Active)

- AnyoneAI - ML/AI course
- Bird streaming - Elixir streaming project
- Elixir Dev Bootcamp - Learning Elixir
- Farmacia - Pharmacy project
- JejoBot - Bot project
- Museum App - Museum application
- Uway - Project

### Current Areas (Ongoing)

- Blog - Content publishing
- Indie Hacker - Side business ventures
- Journal - Personal journaling
- Trading - Trading activities
- Secops & Bugbounty - Security research
- Photography, Music - Creative hobbies

### Resource Topics

AI, Backend, Blockchain, CS & Algorithms, Elixir, Javascript, Python, Rust, PKM

## Do Not

- Modify `.obsidian/` folder
- Break existing `[[wikilinks]]`
- Create files outside the PARA structure without reason
- Make rapid successive edits (iCloud sync issues)

## Progressive Summarization

When distilling notes, apply layers:
1. Original content (captured)
2. **Bold** the main points
3. ==Highlight== the critical parts
4. Add summary at the top

## Weekly Review Support

If asked to help with weekly review:
1. List items in `0 - Inbox/` needing organization
2. Check `1 - Projects/` for completable items → move to Archives
3. Identify stale content for archiving
