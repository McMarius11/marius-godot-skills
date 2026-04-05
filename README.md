# marius-godot-skills

Selbstverbesserndes Agent-System für Godot 4 Entwicklung mit MCP Pro Integration.

## Was ist das?

Ein Claude Code Plugin mit Agents die sich über die Zeit verbessern.
Nach jeder Session fließen Learnings zurück ins System. Agents werden
automatisch gepatcht wenn sie etwas verpasst haben. Je mehr du es nutzt,
desto besser werden die Reviews.

## Einrichten

### Option 1: Claude Code Marketplace

```bash
/plugin marketplace add McMarius11/marius-godot-skills
/plugin install marius-godot-skills
```

### Option 2: Manuell (wenn du lokal dran arbeiten willst)

```bash
git clone https://github.com/McMarius11/marius-godot-skills.git ~/marius-godot-skills
ln -s ~/marius-godot-skills ~/.claude/plugins/marius-godot-skills
```

### Voraussetzungen

- Claude Code mit Claude Max
- Godot 4.x mit Jolt Physics
- Godot MCP Pro Plugin (für Live-Editor-Integration)

## Benutzung

### Neues Projekt starten

```
/init-project
```

Fragt nach Projektname, Spieltyp und Referenz-Stil, erstellt eine CLAUDE.md
mit Kollisionsschichten, Schlüsseldateien und Agenten-Workflow.
Projektspezifische Agents (z.B. quake-verifier) werden bei Bedarf ins Projekt kopiert.

### Während der Arbeit

Nach jeder größeren Implementierung:

```
/review
```

Startet den kompletten Review-Zyklus:
1. **code-reviewer** + **test-runner** laufen parallel
2. Bei Scene-Änderungen (.tscn): **scene-inspector** prüft den Live-Editor
3. Bei _process/_physics_process Code: **performance-reviewer** misst FPS, Draw Calls, Memory
4. Bei Movement/Combat (wenn quake-verifier vorhanden): **quake-verifier** testet Gameplay-Werte

Alle Agents nutzen Godot MCP Pro für Live-Validierung im Editor – Scene starten,
Properties lesen, Input simulieren, Error-Log prüfen. CLI-Checks als Fallback
wenn der Editor nicht offen ist.

### Session beenden

```
/session-end
```

Macht zwei Sachen:
1. **Projekt dokumentieren** – CLAUDE.md aktualisieren, TODOs in docs/todos.md schreiben
2. **Skills-Repo füttern** – Learnings, Gotchas und Agent-Feedback in knowledge/ schreiben

Wenn ein Agent etwas verpasst hat, landet das automatisch in `knowledge/agent-feedback.md`.
Wenn MCP Pro Tools nicht funktioniert haben, landet das in `knowledge/mcp-issues.md`.

## Wie es besser wird

Das System ist nicht statisch. Es lernt aus jeder Session.

### Der Verbesserungsloop

```
Session → Agents arbeiten → session-closer dokumentiert
                                    ↓
                          knowledge/ wird gefüttert
                          (learnings, gotchas, feedback, mcp-issues)
                                    ↓
              ┌─────────────────────┼─────────────────────┐
              ↓                                           ↓
    /improve → self-improver              /mcp-report → Report für
    patcht Agents                         MCP Pro Entwickler
              ↓
    git commit → nächste Session profitiert
```

### Agents verbessern

Wenn ein Agent etwas übersieht oder einen False Positive liefert:

```
/improve
```

Der **self-improver** liest `knowledge/agent-feedback.md`, patcht die betroffenen
Agents und dokumentiert jede Änderung in `knowledge/changelog.md`.

Danach committen damit die nächste Session profitiert:

```bash
cd ~/marius-godot-skills
git add -A && git commit -m "agent patches from session feedback"
git push
```

### Wissen akkumuliert sich

Jede Session füttert automatisch die Wissensbasis:

| Datei | Was reinkommt | Wann |
|-------|---------------|------|
| `learnings.md` | Projektübergreifende Erkenntnisse | Jede Session |
| `patterns.md` | Bewährte Code-Patterns (ab 3+ Erwähnungen befördert) | Via /improve |
| `antipatterns.md` | Was konsistent schiefgeht | Jede Session |
| `godot-gotchas.md` | Godot-spezifische Fallen | Wenn entdeckt |
| `agent-feedback.md` | Was Agents verpasst haben | Jede Session |
| `mcp-issues.md` | MCP Pro Bugs und Feature-Wünsche | Wenn aufgetreten |

Agents lesen diese Dateien vor jedem Review – sie kennen also die gesammelten
Erfahrungen aus allen bisherigen Projekten.

### MCP Pro Feedback

Wenn MCP Pro Tools fehlschlagen oder ein Feature fehlt:

```
/mcp-report
```

Generiert einen sauberen englischen Bug-/Feature-Report aus `knowledge/mcp-issues.md`
den du direkt an den MCP Pro Entwickler schicken kannst.

## Agents

| Agent | Model | Was er macht |
|-------|-------|-------------|
| **code-reviewer** | Opus | Magic Numbers, Architektur, GDScript Best Practices, Signal-Audit via MCP, Dependency-Analyse |
| **test-runner** | Haiku | Error-Log, Scene starten/stoppen, Property-Assertions, Profiling Quick-Check, CLI-Fallback |
| **performance-reviewer** | Sonnet | Live FPS/Draw Calls/Memory, Scene-Complexity, Runtime-Inspektion, Frame-Capture |
| **scene-inspector** | Sonnet | Scene-Tree Struktur, Node-Referenzen, Signal-Verbindungen, Collision-Layer, Gruppen |
| **session-closer** | Sonnet | Projekt-CLAUDE.md + Skills-Repo knowledge/ füttern, MCP-Issues sammeln |
| **self-improver** | Opus | Agent-Feedback verarbeiten, Agents patchen, Knowledge konsolidieren |
| **quake-verifier** | Opus | Quake-1-Treue prüfen – Movement/Waffen/Monster via MCP Input-Simulation (projektspezifisch) |

## Slash Commands

| Command | Was es macht |
|---------|-------------|
| `/review` | Vollständiger Review-Zyklus (alle relevanten Agents) |
| `/session-end` | Session dokumentieren + Learnings ins Skills-Repo |
| `/improve` | Self-Improver: Agents patchen basierend auf Feedback |
| `/init-project` | Neues Projekt mit CLAUDE.md und Ordnerstruktur einrichten |
| `/mcp-report` | MCP Pro Issue-Report für den Entwickler generieren |

## Verzeichnisstruktur

```
.claude-plugin/   Plugin-Manifest für Claude Code Marketplace
agents/           Agents mit YAML Frontmatter
commands/         Slash-Commands
templates/        CLAUDE.md Templates für neue Projekte
knowledge/        Wachsende Wissensbasis
  ├── learnings.md        Cross-Projekt Erkenntnisse
  ├── patterns.md         Bewährte Patterns
  ├── antipatterns.md     Was konsistent schiefgeht
  ├── godot-gotchas.md    Godot-spezifische Fallen
  ├── agent-feedback.md   Inbox für den self-improver
  ├── mcp-issues.md       MCP Pro Bugs/Features/Vorschläge
  └── changelog.md        Agent-Änderungshistorie
CLAUDE.md         Meta-CLAUDE.md für das Skills-Repo selbst
```

## Lizenz

MIT – siehe [LICENSE](LICENSE)
