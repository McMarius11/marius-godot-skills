---
name: mcp-report
description: Erstelle einen sauberen Bug-/Feature-Report aus den gesammelten MCP Pro Issues für den Entwickler
---

Lies knowledge/mcp-issues.md und erstelle einen Report:

1. Filtere nur Einträge mit Status 🆕 (noch nicht gemeldet)
2. Gruppiere nach Kategorie (FEHLT, BROKEN, UNERWARTET, VORSCHLAG)
3. Formatiere als sauberen, höflichen englischen Text (der Entwickler spricht Englisch)
4. Füge technische Details hinzu: Godot-Version, MCP Pro Version (wenn bekannt), OS
5. Setze den Status der gemeldeten Issues auf 📧

Format des Reports:
```
Hi,

I'm using Godot MCP Pro with Claude Code for [Projekttyp] development.
Here are some issues and suggestions I've collected:

## Bugs
[...]

## Missing Features
[...]

## Suggestions
[...]

Setup: Godot [Version], MCP Pro [Version], [OS]
```

Den Report als Markdown-Datei speichern UND in der Konsole ausgeben
damit er direkt kopiert werden kann.
