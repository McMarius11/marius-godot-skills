---
name: review
description: Vollständigen Review-Zyklus starten – Code, Tests, Performance, Scene
---

Starte den kompletten Review-Zyklus:

1. PARALLEL: code-reviewer + test-runner aktivieren
2. Wenn .tscn Dateien geändert: scene-inspector aktivieren
3. Wenn _process/_physics_process betroffen: performance-reviewer aktivieren
4. Wenn Movement/Combat/Waffen betroffen UND quake-verifier existiert: quake-verifier aktivieren

Lies die CLAUDE.md des Projekts für den spezifischen Agenten-Workflow –
der kann von diesem Standard abweichen.

Fasse am Ende alle Findings zusammen und gruppiere nach Priorität.
