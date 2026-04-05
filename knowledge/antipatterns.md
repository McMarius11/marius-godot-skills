# Antipatterns

Ansätze die konsistent schiefgehen. Agents nutzen das als Negativliste.

---

### Antipattern: Magic Number Konstante
Eine Konstante die nur eine Magic Number umbenennt ohne Kontext zu geben.
```gdscript
# ❌ Schlecht
const SPEED = 320  # Was ist 320? Warum dieser Wert?

# ✅ Besser
const GROUND_MOVE_SPEED_QU: float = 320.0  # Quake-Referenz: sv_maxspeed
```

### Antipattern: get_node() in _process
Jeden Frame den Node-Tree durchsuchen statt einmal cachen.
```gdscript
# ❌ Schlecht
func _process(delta: float) -> void:
    get_node("Player").position  # Sucht jeden Frame

# ✅ Besser
@onready var player: CharacterBody3D = $Player
func _process(delta: float) -> void:
    player.position
```

### Antipattern: Stille Fehler
Fehler schlucken statt loggen. Führt zu stundenlangem Debugging.
```gdscript
# ❌ Schlecht
var node = get_node_or_null("MaybeExists")
if node:
    node.do_thing()
# Kein else – wenn fehlt weiß niemand warum es nicht funktioniert

# ✅ Besser
var node = get_node_or_null("MaybeExists")
if not node:
    push_warning("MaybeExists nicht gefunden – Feature X deaktiviert")
    return
node.do_thing()
```
