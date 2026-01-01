# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Type

This is an Obsidian vault - a personal knowledge management system for note-taking and documentation. Obsidian is a markdown-based note-taking app that stores all data locally as plain text files.

## Vault Structure

```
Documents/Personal/
├── .obsidian/           # Vault configuration (do not modify directly)
├── AI/                  # AI-related notes
├── Blockchain/          # Blockchain, Ethereum, Polkadot notes
├── CS & Algorithms/     # Computer science and algorithms
├── Elixir/              # Elixir programming notes and bootcamp content
├── Excalidraw/          # Diagrams and drawings
├── Indie Hacker/        # Indie hacking ideas and resources
├── Javascript/          # JS, React, Next.js, TypeScript notes
├── PKM/                 # Personal knowledge management, resources
├── Rust/                # Rust programming notes
├── Trading/             # Trading journal and strategies
└── [various .md files]  # Standalone notes
```

## Working with Obsidian Vaults

### File Format
- All notes are Markdown files (.md)
- Frontmatter (YAML at the top of files) is used for metadata
- Excalidraw files use `.excalidraw.md` extension

### Obsidian-Specific Syntax
- **Internal Links:** `[[Note Name]]` creates links between notes
- **Aliases:** `[[Note Name|Display Text]]` for custom link text
- **Embeds:** `![[Note Name]]` embeds content from another note
- **Tags:** `#tag` for categorization
- **Block References:** `[[Note#^block-id]]` links to specific blocks

### Installed Plugins
- **Excalidraw:** Drawing and diagramming
- **Dataview:** Query notes like a database
- **Tasks:** Task management with checkboxes
- **Templater:** Template system for notes
- **Omnisearch:** Enhanced search
- **Readwise:** Sync highlights from reading apps
- **Ink:** Handwriting support

## Important Considerations

- **Preserve link formats:** When editing notes, maintain `[[wikilink]]` syntax - changing note names can break links
- **Avoid modifying .obsidian/:** This folder contains vault settings, plugins, and themes
- **iCloud sync:** This vault syncs via iCloud - avoid creating conflicts with rapid edits
- **Frontmatter:** Respect existing YAML frontmatter structure when present
