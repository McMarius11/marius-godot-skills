# Godot Gotchas

Godot-spezifische Fallen die in Projekten aufgefallen sind.
Agents nutzen das um bekannte Probleme zu erkennen.

---

### Gotcha: call_deferred bei Node-Löschung in Physics
Node-Löschung/Manipulation in physics_process kann zu Crashes führen.
Immer call_deferred() oder queue_free() nutzen, nie direkte Manipulation.

### Gotcha: Autoload-Abhängigkeiten in --check-only
`godot --headless --check-only --script` kann Scripts mit Autoload-Abhängigkeiten
nicht prüfen. Gibt Fehler aus die keine echten Fehler sind.
Lösung: Projekt-weiten Check als Fallback nutzen.

### Gotcha: Signal-Verbindungen in _ready vs Editor
Signals können sowohl im Editor als auch in _ready() verbunden werden.
Doppelte Verbindungen führen zu doppelten Aufrufen.
Prüfen: Ist das Signal schon im Editor verbunden?

### Gotcha: Jolt Physics vs Default
Jolt verhält sich in Edge Cases anders als Godot-Default-Physics.
Besonders bei: Stair-Stepping, Bounce-Verhalten, Sleep-Thresholds.
