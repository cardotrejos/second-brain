# CLAUDE.md

This file provides guidance to Claude Code when working with this Obsidian vault.

## Project Type

This is an Obsidian vault using the **Building a Second Brain (BASB)** methodology with the PARA system for organization.

## PARA Structure

```
Documents/Personal/
├── .obsidian/           # Vault config (do not modify)
├── 0 - Inbox/           # Quick capture, unsorted notes
├── 1 - Projects/        # Active work with defined endpoints
│   ├── AnyoneAI/
│   ├── Bird streaming/
│   ├── Elixir Dev Bootcamp/
│   ├── Farmacia/
│   ├── JejoBot/
│   ├── Museum App/
│   └── Uway/
├── 2 - Areas/           # Ongoing responsibilities (no end date)
│   ├── Blog/
│   ├── Indie Hacker/
│   ├── Journal/
│   ├── Music/
│   ├── Photography/
│   ├── Productivity/
│   ├── Secops & Bugbounty/
│   └── Trading/
├── 3 - Resources/       # Reference material by topic
│   ├── AI/
│   ├── Backend/
│   ├── Blockchain/
│   ├── CS & Algorithms/
│   ├── Elixir/
│   ├── Excalidraw/
│   ├── Ink/
│   ├── Javascript/
│   ├── PKM/
│   ├── Python/
│   ├── Rust/
│   └── Attachments/
└── 4 - Archives/        # Completed/inactive items
```

## PARA Decision Tree

When creating or organizing notes:

1. **Actionable with deadline?** → `1 - Projects`
2. **Ongoing responsibility?** → `2 - Areas`
3. **Reference material?** → `3 - Resources`
4. **Done or inactive?** → `4 - Archives`
5. **Unsure?** → `0 - Inbox`

## Working with This Vault

### Creating Notes
- New notes go in `0 - Inbox/` unless clearly belonging elsewhere
- Use descriptive filenames (will become note titles)
- Add YAML frontmatter for metadata when appropriate

### Obsidian Syntax
- **Links:** `[[Note Name]]` or `[[Note Name|Display Text]]`
- **Embeds:** `![[Note Name]]` embeds content
- **Tags:** `#tag` for categorization
- **Block refs:** `[[Note#^block-id]]` for specific blocks

### File Types
- Notes: `.md` (Markdown)
- Drawings: `.excalidraw.md`
- Attachments: Images/PDFs in `3 - Resources/Attachments/`

### Installed Plugins
- Excalidraw, Dataview, Tasks, Templater
- Omnisearch, Readwise, Ink

## Important Rules

1. **Preserve wikilinks** - changing note names breaks `[[links]]`
2. **Never modify `.obsidian/`** - contains vault settings
3. **Avoid rapid edits** - vault syncs via iCloud
4. **Respect frontmatter** - keep existing YAML structure
5. **Follow PARA** - organize by actionability, not topic

## CODE Workflow

When helping with notes, follow the CODE method:

- **Capture:** Save to Inbox first, organize later
- **Organize:** Move to correct PARA folder
- **Distill:** Bold key points, highlight essentials, summarize at top
- **Express:** Help create outputs from collected notes
