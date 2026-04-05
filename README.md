# marius-godot-skills

Selbstverbesserndes Agent-System für Godot 4 Entwicklung mit MCP Pro Integration.

## Was ist das?

Ein Claude Code Plugin mit Agents die sich über die Zeit verbessern.
Nach jeder Session fließen Learnings zurück ins System. Agents werden
automatisch gepatcht wenn sie etwas verpasst haben.

## Installation

```bash
# Option 1: Claude Code Marketplace
/plugin marketplace add <github-user>/marius-godot-skills
/plugin install marius-godot-skills

# Option 2: Manuell
git clone <repo-url> ~/marius-godot-skills
# Symlink in Claude Code:
ln -s ~/marius-godot-skills ~/.claude/plugins/marius-godot-skills
```

## Agents

| Agent | Model | Zweck |
|-------|-------|-------|
| code-reviewer | Opus | Code-Qualität, Architektur, GDScript Best Practices |
| test-runner | Haiku | Syntax-Checks, Scene-Tests, Error-Log, Profiling |
| performance-reviewer | Sonnet | Live-Profiling, Frame-Budget, Memory-Leaks |
| scene-inspector | Sonnet | Scene-Tree, Signals, Collision-Layer, Resources |
| session-closer | Sonnet | Projekt-Doku + Skills-Repo Feedback-Loop |
| self-improver | Opus | Patcht Agents basierend auf gesammeltem Feedback |
| quake-verifier | Opus | Quake-1-Treue (projektspezifisch) |

## Slash Commands

| Command | Zweck |
|---------|-------|
| `/review` | Vollständiger Review-Zyklus |
| `/session-end` | Session abschließen + Learnings erfassen |
| `/improve` | Self-Improver aktivieren |
| `/init-project` | Neues Projekt mit CLAUDE.md einrichten |
| `/mcp-report` | MCP Pro Issue-Report für den Entwickler generieren |

## Der Verbesserungsloop

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

## Verzeichnisstruktur

```
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
```

## Voraussetzungen

- Claude Code mit Claude Max
- Godot 4.x mit Jolt Physics
- Godot MCP Pro Plugin (für Live-Editor-Integration)
