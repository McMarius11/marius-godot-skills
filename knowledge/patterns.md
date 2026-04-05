# Bewährte Patterns

Code- und Architektur-Patterns die sich projektübergreifend bewährt haben.
Werden von Agents als Referenz genutzt.

---

### Pattern: Defensive _ready()
Immer prüfen ob Nodes existieren bevor sie genutzt werden.
```gdscript
@onready var weapon_manager: WeaponManager = $WeaponManager as WeaponManager

func _ready() -> void:
    if not weapon_manager:
        push_error("WeaponManager nicht gefunden")
        return
```

### Pattern: Signal-basierte Entkopplung
Statt direkter Node-Referenzen Signals nutzen. Hält Systeme austauschbar.
```gdscript
signal health_changed(new_health: int)
# Statt: $HUD.update_health(health)
health_changed.emit(health)
```

### Pattern: Konstanten-Klasse pro System
Nicht in jeder Datei eigene Konstanten, sondern zentral pro System.
```gdscript
class_name PlayerConstants
const GROUND_SPEED: float = 320.0
const JUMP_VELOCITY: float = 270.0
const GRAVITY: float = 800.0
```
