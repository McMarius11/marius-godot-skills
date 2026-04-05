---
name: init-project
description: Neues Godot-Projekt mit CLAUDE.md, Ordnerstruktur und Agent-Workflow einrichten
---

Richte ein neues Godot-Projekt für die Arbeit mit den Skills ein:

1. Frage nach: Projektname, Spieltyp (FPS, etc.), Referenz-Stil (Quake, Duke, etc.)
2. Kopiere templates/CLAUDE.md.template → CLAUDE.md und fülle die Platzhalter
3. Erstelle docs/ Ordner mit todos.md
4. Wenn FPS mit Quake-Referenz: Kopiere den quake-verifier Agent ins Projekt unter .claude/agents/
5. Erstelle .claude/settings.json mit MCP Pro Konfiguration falls nötig

Prüfe ob marius-godot-skills als Plugin installiert ist.
Wenn nicht: erkläre wie man es installiert.

Am Ende: Zeige eine Zusammenfassung was eingerichtet wurde und welche Agents aktiv sind.
