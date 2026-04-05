# marius-godot-skills — CLAUDE.md

## Was ist das?
Ein lebendes Agent-System für Godot 4 Entwicklung.
Die Agents hier sind NICHT statisch – sie verbessern sich über die Zeit.
Jede Session bringt neues Wissen, jedes Problem verbessert die Agents.

## Repo-Struktur
```
agents/           → Claude Code Agents (.md mit YAML Frontmatter)
commands/         → Slash-Commands für Claude Code (/review, /session-end, /improve, /init-project)
templates/        → CLAUDE.md Templates für neue Projekte
knowledge/        → Wachsende Wissensbasis (cross-project Learnings)
```

## Verbesserungsloop
Der Kreislauf der dieses System am Leben hält:

1. **Session**: Agents werden in einem Godot-Projekt genutzt
2. **Session-Ende**: session-closer dokumentiert was passiert ist
3. **Feedback**: Wenn ein Agent was verpasst hat → in knowledge/learnings.md notieren
4. **Verbesserung**: /improve oder self-improver Agent patcht die Agents
5. **Commit**: Änderungen committen → nächste Session profitiert

## Regeln für Änderungen an diesem Repo
- NIEMALS einen Agent verschlechtern – nur erweitern oder präzisieren
- Jede Änderung an einem Agent braucht einen Grund in knowledge/changelog.md
- Neue Patterns immer in knowledge/patterns.md dokumentieren
- Neue Godot-Pitfalls in knowledge/godot-gotchas.md
- Wenn ein Check einen False-Positive hatte → Ausnahme dokumentieren, nicht Check entfernen
- Agents bleiben unter 100 Zeilen – wenn länger, auslagern in knowledge/

## Knowledge-Dateien
| Datei | Zweck |
|-------|-------|
| knowledge/learnings.md | Was in Projekten gelernt wurde |
| knowledge/patterns.md | Bewährte Code-/Architektur-Patterns |
| knowledge/antipatterns.md | Was konsistent schiefgeht |
| knowledge/godot-gotchas.md | Godot-spezifische Fallen |
| knowledge/changelog.md | Änderungshistorie der Agents |
| knowledge/mcp-issues.md | MCP Pro Bugs, fehlende Features, Vorschläge |
